pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Compiling the code...'
                sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn clean test'
            }
        }
        
        stage('Package') {
            when {
                expression {
                    return env.BRANCH_NAME == 'master'
                }
            }
            steps {
                echo 'Generating artifacts...'
                sh 'mvn package -DskipTests'
                archiveArtifacts 'target/*.war'
            }
        }
        
        stage('Docker BnP') {
            when {
                expression {
                    return env.BRANCH_NAME == 'master'
                }
            }
            steps {
                echo 'Building and publishing Docker images...'
                // Add your Docker build and push steps here
            }
        }
    }
    
    tools {
        maven 'Maven 3.6.3'
    }
    
    post {
        always {
            echo 'This pipeline is completed.'
        }
    }
}
