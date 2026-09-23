pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                sh './gradlew check'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
    }

    post {
        always {
            junit 'app/build/test-results/**/*.xml'

            archiveArtifacts artifacts: 'app/build/libs/*.jar',
                             fingerprint: true

            echo 'Cleaning up workspace...'
            deleteDir()
        }

        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            mail to: 'team@example.com',
                 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                 body: "Something is wrong with ${env.BUILD_URL}"
        }
    }
}