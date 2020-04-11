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
                python -m pip install molecule
                python -m pip install docker
                
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
        stage("converge") {
            steps {
                sh """
                    source ./env/bin/activate 
                    molecule converge
                """
            }
        }
        stage("verify") {
            steps {
                sh """
                    source ./env/bin/activate 
                    molecule verify
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