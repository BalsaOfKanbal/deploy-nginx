pipeline {
    agent {
        label 'generic'
    }
    stages {
        stage('install dependencies') {
            steps {
                sh """
                python3 -m venv env
                source ./env/bin/activate 
                python -m pip3 install google-assistant-sdk[samples]
                sudo pip3 install molecule
                sudo pip3 install docker
                """
            }
        }
        stage('lint') {
            steps {
                sh """
                    source ./env/bin/activate 
                    molecule lint
                """
            }
        }
        stage('create') {
            steps {
                sh """
                    source ./env/bin/activate 
                    molecule create
                """
            }
        }
        stage("idempotence") {
            steps {
                sh """
                    source ./env/bin/activate 
                    molecule idempotence
                """
            }
        }
        stage("cleanup") {
            steps {
                sh """
                    source ./env/bin/activate 
                    molecule verify
                """
            }
        }
        stage("destroy") {
            steps {
                sh """
                    source ./env/bin/activate 
                    molecule destroy
                """
            }
        }

    }
    post {
        always {
            sh """
                rm -rf env
            """
        }
    }
}