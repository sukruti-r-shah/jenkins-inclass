pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                sh './gradlew check'
            }
        }
    }

    post {
        always {
            junit 'app/build/test-results/**/*.xml'
        }
    }
}