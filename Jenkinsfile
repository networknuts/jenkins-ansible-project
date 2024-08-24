pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code repository
                git branch: 'main',
                    url: 'https://github.com/networknuts/jenkins-ansible-project.git'
            }
        }
        
        stage('Verify Ansible Installation') {
            steps {
                // Install required packages and dependencies
                sh 'whereis ansible-lint'
                sh 'whereis ansible-playbook'
            }
        }
        
        stage('Linting') {
            steps {
                // Run Ansible playbook syntax check and linting
                sh 'ansible-playbook playbook.yml -i inventory --syntax-check'
                sh 'ansible-lint playbook.yml'
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                // Run the Ansible playbook
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }
    }
    
    post {
        always {
            // Archive the Ansible playbook execution logs
            archiveArtifacts '*.log'
        }
        
        success {
            // Notify success
            echo 'Ansible playbook executed successfully!'
        }
        
        failure {
            // Notify failure
            echo 'Ansible playbook execution failed!'
        }
    }
}
