def buildVersion

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from version control
                git url: 'https://github.com/gayathri-ja/weatherapprepo.git', 
                    credentialsId: '1b5ef133-eaa9-4d11-97c5-82329c8aa60c',
                    branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Generate a timestamp-based version number for the Docker image.
                script {
                    buildVersion = new Date().format('yyyyMMdd-HHmmss')
                }

                // Build your Docker image with the version number
                sh "docker build -t gayathrija/weatherappdev:${buildVersion} ."
            }
        }

        stage('Unit Test') {
            steps {
                // Run your unit tests inside the Docker container
                sh "docker run --rm gayathrija/weatherappdev:${buildVersion} pytest test_app.py"
            }
        }

        stage('Deploy') {
            steps {
                script {
                    DOCKERHUB_CREDENTIALS = credentials('ac643925-fe10-4d90-899c-4282fae6dc00')
                }
                
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                // Push the Docker image to a container registry 
                sh 'docker push gayathrija/weatherappdev:${buildVersion}'
                        
                // Log in to Docker Hub using the credentials
                
                
                // Push the Docker image to a container registry
                
               

                // Deploy the application using the Docker image
                // You might use Docker Compose, Kubernetes, or other deployment methods based on your setup.
                // Here's an example using Docker Compose:
                
            }
        }
    }
}
