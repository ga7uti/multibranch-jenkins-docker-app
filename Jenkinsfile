pipeline{
    agent{
        docker {
            image 'maven:3.8.2-jdk-8'
        }
    }
    stages{
        stage("Test"){
            steps{
                sh 'mvn --version'
            }
        }
    }
}