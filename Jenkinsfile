pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = "False"
        PATH = "$PATH:/home/jenkins/.local/bin"
    }

    stages {

        stage('Install Ansible & Docker modules') {
            steps {
                sh '''
                python3 --version
                python3 -m pip install --user --upgrade pip
                python3 -m pip install --user ansible community.docker
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
