pipeline {
    agent {
        label 'generic'
    }
    stages {
        stage('install dependencies') {
            steps {
                sh """
                    pip3 install molecule
                    pip3 install docker
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
                sudo pip3 uninstall molecule -y
                sudo pip3 uninstall docker -y
            """
        }
    }
}