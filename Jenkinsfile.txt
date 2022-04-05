pipeline{
    agent{label 'slave_static'}
    tools {
        jdk 'JAVA9'
        maven 'M3'
    }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/LiliiaKoloda/SpringPetClinic.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Deploy'){
            steps{
                sh 'java -jar /var/lib/jenkins/workspace/PetClinicDeclarativePipeline/target/*.jar'
            }
        }
    }
}