pipeline{
    agent{
        docker {
            image 'maven:3.8.2-jdk-8'
        }
    }
    environment {
        HOME="."
    }
    stages{
        stage("Compile"){
            steps{
                sh 'mvn compile'
            }
        }
        
        stage("Test"){
            steps{
                sh 'mvn test'
            }
        }
        
        stage("Package"){
            steps{
                sh 'mvn package'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'dev'
            }
            steps {
                echo 'Deliver for development'
                script {
                            withCredentials([sshUserPrivateKey(credentialsId: 'ec2_credentials', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'ec2-user')]) {
                            def remote = [:]
                            remote.name = 'ec2-user'
                            remote.host = 'ec2-52-66-206-100.ap-south-1.compute.amazonaws.com'
                            remote.allowAnyHosts = true
                            remote.user = 'ec2-user'
                            remote.identityFile = identity
                            sshPut remote: remote, from: 'deploy.sh', into: '/home/ec2-user/'
                            sshCommand remote: remote, command: 'cd /home/ec2-user/; chown ec2-user: deploy.sh; chmod +x deploy.sh'
                            sshCommand remote: remote, command: 'rm /home/ec2-user/*.jar', failOnError:'false'
                            sshPut remote: remote, from: 'target/jenkins-app-0.0.1-SNAPSHOT.jar', into: '/home/ec2-user/'
                            sshCommand remote: remote, command: 'cd /home/ec2-user/;dos2unix deploy.sh;sudo ./deploy.sh'
                            sshRemove remote: remote, path: '/home/ec2-user/deploy.sh'
                            }
                }
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                script{
                   sshPut remote: remote, from: 'kill.sh', into: '/home/ec2-user/'
                   sshCommand remote: remote, command: 'cd /home/ec2-user/; chown ec2-user: kill.sh; chmod +x kill.sh'
                   sshCommand remote: remote, command: 'cd /home/ec2-user/;dos2unix kill.sh;sudo ./kill.sh'
                   sshRemove remote: remote, path: '/home/ec2-user/kill.sh'

                }
            }
        }
        stage('Deliver for production') {
            when {
                branch 'prod'
            }
            steps {
                echo 'Deliver for production'
            }
        }
    }
}