pipeline {
    agent {label 'DevOps'}
    stages {
        stage('Install python') {
            steps {
                sh """ 
                    apt-get update
                    apt-get install python3 python3-pip -y
                """
            }

        }
        stage('Install dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }

        }
        stage('Run pytest') {
            steps {
                sh 'coverage run -m pytest'
            }
        }
        stage('Run Coverage pytest') {
            steps {
                sh 'coverage html'
            }
        }
    }
}