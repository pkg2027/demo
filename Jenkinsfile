pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/pkg2027/demo.git']]
                )
            }
        }

        stage('Permission') {
            steps {
                sh '''
                    chmod 711 pre-run.sh
                    chmod 711 data.sh
                    sleep 2
                '''
            }
        }

        stage('System Check') {
            steps {
                sh '''
                    ./pre-run.sh
                    sleep 2
                '''
            }
        }

        stage('Running Shell') {
            steps {
                sh '''
                    ./data.sh >> data.txt 2>&1
                    sleep 5
                '''
            }
        }

        stage('Final Stage') {
            steps {
                echo "PIPELINE COMPLETED!!!"
            }
        }
    }

    post {
        always {
            echo "🧹 Cleaning up workspace..."
            deleteDir()
        }
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check console output for details."
        }
        unstable {
            echo "⚠️ Pipeline marked as unstable. Review logs."
        }
        aborted {
            echo "⏹️ Pipeline was aborted by user."
        }
    }
}
