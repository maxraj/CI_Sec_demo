pipeline {
    agent any
    
    stages {
        stage('Init Env') {
            steps {
                
                checkout scm
                
                sh 'echo test setup has started'
                sh 'docker stop gruyere || true'
                sh 'docker pull gauntlt/gauntlt'
                sh 'docker pull karthequian/gruyere:latest'
                sh 'docker run --rm -d -p 8008:8008 --name gruyere karthequian/gruyere:latest'
                sh 'docker ps -a'
                
            }
        }
        stage('Test for security issues') {
            steps {
                sh 'chmod +x ./scripts/ip-config.sh'
                sh './scripts/ip-config.sh'
                sh 'cat ./config/cucumber.yml'
                sh 'docker run -t --rm -v $(pwd):/working -w /working gauntlt/gauntlt ./Tests/xss.attack'
            }
        }
    }
}
