@Library('Shared') _

pipeline {
    agent {
        label 'vinod'
    }

    triggers {
        githubPush()
    }

    stages {

        stage('Hello') {
            steps {
                script {
                    hello()
                }
            }
        }

        stage('Code Clone') {
            steps {
                script {
                    clone('https://github.com/abdalihuzaifasyed/django-notes-app.git', 'main')
                }
            }
        }

        stage('Code Build') {
            steps {
                script {
                    dockerbuild('notes-app', 'latest')
                }
            }
        }

        stage('Code Test') {
            steps {
                script {
                    runtests()
                }
            }
        }

        stage('Push On Docker Hub') {
            steps {
                script {
                    dockerpush('dockerHubCred', 'notes-app', 'latest')
                }
            }
        }

        stage('Code Deploy') {
            steps {
                script {
                    deploy()
                }
            }
        }
    }
}
