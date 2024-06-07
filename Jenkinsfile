pipeline {
    agent any

    stages {
        stage('Pull form Github and install deps') {
            steps {
                git branch: 'main', credentialsId: 'ID_Jenkins', url: 'https://github.com/Tidaly-IO/tidaly-backend.git'
                sh 'cd backend && docker build -t ghcr.io/tidaly-io/backend .'
                sh 'docker tag ghcr.io/tidaly-io/backend:latest ghcr.io/tidaly-io/backend:latest'
                sh 'docker login ghcr.io -u MaximeMRF -p PASSWORD_HERE'
                sh 'docker push ghcr.io/tidaly-io/backend:latest'
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                ansiblePlaybook(
                    playbook: './backend/deploy.yml',
                    inventory: './backend/inventory.ini'
                )
            }
        }
    }
}
