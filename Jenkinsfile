pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'stanmarek'
        DOCKERHUB_PASSWORD = 'gigasilnehaslo'
    }

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
                    sh 'echo Deploying'
                    sh 'docker build -t stanmarek/devops-golang-project -f Dockerfile.deploy .'
                }
            }
            post {
                success {
                    sh 'echo Deploy finished'
                }
                failure {
                    sh 'echo Deploy failure'
                }
            }
        }
        stage('Publish') {
            agent any
            steps {
                // withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPassword', usernameVariable: 'dockerhubUser')])
                sh 'docker login -u ${DOCKERHUB_USER} -p ${DOCKERHUB_PASSWORD}'
                sh 'docker push stanmarek/devops-golang-project'
            }
        }
    }
}
