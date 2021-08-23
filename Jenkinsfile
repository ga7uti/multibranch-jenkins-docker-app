pipeline{
    agent{
        docker {
            image 'maven:3.8.2-jdk-8'
        }
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
    }
}