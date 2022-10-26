pipeline {
    agent {label 'DevOps'}
    environment {
                    SONAR_TOKEN = credentials('sonarqube')
                }
    stages {
        stage('Install python') {
            steps {
                sh """ 
                    sudo apt-get update
                    sudo apt-get install python3 python3-pip -y
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
                sh 'python3 -m coverage run -m pytest'
            }
        }
        stage('Run Coverage pytest') {
            steps {
                sh 'python3 -m coverage html'
            }
        }
        stage('Static code analysis') {
            steps {
                script {
                    def sonarscannerParams = "-Dsonar.login=${SONAR_TOKEN}"
                    sh '/opt/sonar-scanner/sonar-scanner-4.2.0.1873-linux/conf/bin/sonar-scanner ${sonarscannerParams}'
                }
            }
        }
    }
}