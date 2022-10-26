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
                sh """
                    curl -o sonarscanner.zip -L https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.2.0.1873-linux.zip
                    unzip sonarscanner.zip -d /var/opt/sonar-scanner
                    rm sonarscanner.zip
                    echo "sonar.host.url=http://10.0.2.15:3002" > /var/opt/sonar-scanner/sonar-scanner-4.2.0.1873-linux/conf/sonar-scanner.properties
                    /var/opt/sonar-scanner/sonar-scanner-4.2.0.1873-linux/bin/sonar-scanner -Dsonar.login=${SONAR_TOKEN}
                """
            }
        }
    }
}