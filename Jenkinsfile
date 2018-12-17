pipeline {
    agent any
    stages {
        stage('Init Env') {
            steps {
                
                checkout scm
                
                sh 'echo test setup started'
                sh 'sudo docker stop gruyere || true'
                sh 'sudo docker pull karthequian/gruyere:latest'
                sh 'sudo docker pull gauntlt/gauntlt'
                sh 'sudo docker run --rm -d -p 8008:8008 --name gruyere karthequian/gruyere:latest'
                sh 'sudo docker ps -a'
            }
        }
        stage('Test for security issues') {
            steps {
                sh 'sudo chmod +x ./scripts/ip-config.sh'
                sh 'sudo ./scripts/ip-config.sh'
                sh 'cat ./config/cucumber.yml'
                sh 'sudo docker run -t --rm -v $(pwd):/working -w /working gauntlt/gauntlt ./Tests/xss.attack'
            }
        }
    }
}
