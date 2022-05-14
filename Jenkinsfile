pipeline {
    agent any

    stages {
        stage("Fetch dependencies") {
            steps {
                script {
                    sh 'echo Downolading dependencies'
                    sh 'docker build -t project-dep:latest -f Dockerfile.dep .'
                }
            }
            post {
                success {
                    sh 'echo Dependencies downloaded'
                }
                failure {
                    sh 'echo Dependencies downloading failure'
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    sh 'echo Building'
                    sh 'docker build -t project-build:latest -f Dockerfile.build .'
                    // sh 'rm -rf shared'
                    // sh 'mkdir shared'
                    // sh 'docker run project-build:latest -v \$(pwd)/shared:/out'
                    // sh 'ls shared'
                }
            }
            post {
                success {
                    sh 'echo Build finished'
                }
                failure {
                    sh 'echo Build failure'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'echo Testing'
                    sh 'docker build -t project-test -f Dockerfile.test .'
                }
            }
            post {
                success {
                    sh 'echo Tests finished'
                }
                failure {
                    sh 'echo Tests failure'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'echo deploy'
                }
            }
        }
    }
}
