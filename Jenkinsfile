pipeline {
    agent any
    
    environment {
        ANSIBLE_HOST_KEY_CHECKING = "False"
        PATH = "$PATH:/var/jenkins_home/.local/bin"
    }
    
    stages {
        stage('Install Ansible & Docker modules') {
            steps {
                sh '''
                python3 --version
                python3 -m pip install --break-system-packages --user --upgrade pip
                python3 -m pip install --break-system-packages --user ansible requests docker
                ansible-galaxy collection install community.docker --force
                '''
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                sh '''
                ansible --version
                ansible-playbook -i hosts.ini pull_images.yml
                '''
            }
        }
    }
    
    post {
        success {
            echo '✅ Images Docker pull avec succès'
        }
        failure {
            echo '❌ Erreur dans le pipeline'
        }
    }
}