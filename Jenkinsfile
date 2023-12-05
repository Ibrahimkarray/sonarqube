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
                    sh 'docker run -d -p 5000:5000 sonarqube'
                }
            
            }
        }

       stage('SonarQube Analysis') {
    steps {
        script {
            def pomPath = sh(script: 'find . -name pom.xml', returnStdout: true).trim()
            if (pomPath.isEmpty()) {
                error 'No pom.xml found in the workspace.'
            }

            echo "Found pom.xml at: $pomPath"

            // Run SonarQube analysis
            sh "cd ${pomPath.parent} && mvn sonar:sonar"
        }
    }
}
    }
}
