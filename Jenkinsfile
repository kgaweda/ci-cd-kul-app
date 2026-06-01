pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                sh '''
                python3 -m py_compile app.py
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                docker build -t flask-demo .
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop flask-demo || true
                docker rm flask-demo || true

                docker run -d \
                    --name flask-demo \
                    -p 5000:5000 \
                    flask-demo
                '''
            }
        }
    }
}