pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                // Example: git 'https://github.com/your/repository.git'
            }
        }

        stage('Scan with Trufflehog') {
            steps {
                script {
                    // Install Trufflehog if not already installed
                    sh 'pip install trufflehog'

                    // Scan the directory with Trufflehog and save the output to a file
                    sh 'trufflehog --entropy=True /opt/RE-Treat-Final/ > trufflehog_output.txt'
                }
            }
        }

        stage('Scan with Retire.js') {
            steps {
                script {
                    // Install Retire.js if not already installed
                    sh 'npm install -g retire'

                    // Scan the directory with Retire.js and save the output to a file
                    sh 'retire --outputformat text --outputpath retirejs_output.txt /path/to/your/directory'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'trufflehog_output.txt,retirejs_output.txt', allowEmptyArchive: true
            }
        }
    }
}