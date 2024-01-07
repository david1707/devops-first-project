pipeline{
    agent any
    options {
        timeout(time: 3, unit: 'MINUTES') 
    }
    // Go to Dashboard -> Manage Jenkins -> Tools and add 'NodeJS' in your NodeJS section
    tools {nodejs "NodeJS"}
    stages {
        stage('Cloning GitHub Repo'){
            steps{
                git branch: 'main',
                    url: 'https://github.com/david1707/devops-first-project.git'
            }
        }
        
        stage('Install dependencies'){
            options {
                timeout(time: 90, unit: 'SECONDS') 
            }
            steps {
                sh 'npm install'
                sh 'npm install pm2 -g'
            }
            
        }
        /*
        stage('Fixing up') {
            steps {
                sh 'npm audit fix --force'
            }
        }
        */
        stage('Run'){
            steps {
                sh 'pm2 startOrRestart pm2.config.json'
            }
        }
    }
    post { 
        unsuccessful { 
            slackSend color: "danger", message: "The Pipeline build process has failed. Please, check and fix the problem"
        }
        success {
            slackSend color: "good", message: "The Pipeline build process has been a success. Good job!"
        }
    }
}