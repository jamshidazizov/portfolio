pipeline {
    agent any
    
    stages {
        stage('Install Node.js and packages') {
            steps {
                sh 'curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -'
                sh 'sudo apt-get install -y nodejs'
                sh 'npm install'
            }
        }
        stage('Build and deploy') {
            steps {
                sh 'npm run build'
                sh 'npm run deploy'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-creds', usernameVariable: 'GITHUB_USERNAME', passwordVariable: 'GITHUB_TOKEN')]) {
                    sh 'git config --global user.email "jenkins@example.com"'
                    sh 'git config --global user.name "Jenkins"'
                    sh 'git clone -b gh-pages https://${GITHUB_USERNAME}:${GITHUB_TOKEN}@github.com/kimawalo/portfolio.git gh-pages'
                    sh 'cp -r dist/* gh-pages'
                    sh 'cd gh-pages && git add --all && git commit -m "Jenkins build" && git push'
                }
            }
        }
    }
}
