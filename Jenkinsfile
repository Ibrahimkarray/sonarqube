pipeline {
    agent any

    stages {
        
        stage ("Clean up"){
            steps {
                deleteDir()
            }
        }
        
        stage('Pull Repository') {
            steps {
                // Pull the repository source code from Git into the workspace
                git branch: 'main', url: 'https://github.com/Ibrahimkarray/sonarqube.git'
            }
        }

        

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image within the workspace directory
                    sh 'docker build -t sonarqube .'
                }
            
        }
        }

        stage('Run Docker Container') {
            steps {
                
                script {
                    // Run the Flask app in a Docker container within the workspace directory
                    sh 'docker run -d -p 5001:5001 jenkinsflask'
                }
            
            }
        }
    }

    
}
