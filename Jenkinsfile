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
                sh './deploy.sh'
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