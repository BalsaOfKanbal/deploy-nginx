pipeline {
    agent {
        label 'generic'
    }
    stages {
        stage('install dependencies') {
            steps {
                sh """
                    sudo pip install molecule
                    sudo pip install docker
                """
            }
        }
        stage('lint') {
            steps {
                sh """
                    molecule lint
                """
            }
        }
        stage('create') {
            steps {
                sh """
                    molecule create
                """
            }
        }
        stage("idempotence") {
            steps {
                sh """
                    molecule idempotence
                """
            }
        }
        stage("cleanup") {
            steps {
                sh """
                    molecule verify
                """
            }
        }
        stage("destroy") {
            steps {
                sh """
                    molecule destroy
                """
            }
        }

    }
    post {
        always {
            sh """
                sudo pip uninstall molecule -y
                sudo pip uninstall docker -y
            """
        }
    }
}