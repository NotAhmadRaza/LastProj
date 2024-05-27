pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'dsadasf' // Replace with your repository URL
            }
        }

        stage('Deploy to Google Cloud') {
            steps {
                script {
                    try {
                        withCredentials([file(credentialsId: 'keyy', variable: 'GCP_KEY_FILE')]) {
                            sh 'gcloud auth activate-service-account --key-file=$GCP_KEY_FILE'
                            sh 'gcloud config set project genuine-habitat-423301-a2' // Replace with your GCP project ID
                            sh 'gcloud compute ssh ar784419@husnainjenkins --zone=us-central1-a --command="sudo mkdir -p /var/www/html && sudo chmod 777 /var/www/html"' // Create destination directory and set permissions
                            sh 'gcloud compute scp index.html ar784419@husnainjenkins:/var/www/html --zone=us-central1-a' // Copy file to destination directory
                            echo 'Successfully deployed index.html to Google Cloud server'
                        }
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Failed to deploy index.html to Google Cloud server: ${e.message}")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Successfully deployed!'
        }
    }
}
