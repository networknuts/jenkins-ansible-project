pipeline {
    agent any
    
    environment {
        ANSIBLE_VERSION = '2.10.10' // Define the version of Ansible to use
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code repository
                git 'https://github.com/your/repository.git'
            }
        }
        
        stage('Verify Ansible Installation') {
            steps {
                // Install required packages and dependencies
                sh 'whereis ansible-navigator'
                sh 'whereis ansible-playbook'
            }
        }
        
        stage('Linting') {
            steps {
                // Run Ansible playbook syntax check and linting
                sh 'ansible-playbook playbook.yml --syntax-check'
                sh 'ansible-lint playbook.yml'
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                // Run the Ansible playbook
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }
        
        stage('Cleanup') {
            steps {
                // Clean up any temporary files or resources
                sh 'rm -rf some_temporary_files'
            }
        }
    }
    
    post {
        always {
            // Archive the Ansible playbook execution logs
            archiveArtifacts 'logs/*.log'
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
