pipeline {
    agent none  // We’ll assign agents per stage

    tools {
        jdk 'chiomajava'
        maven 'chiomamaven'
    }

    environment {
        REPO_URL = 'https://github.com/Chioma-Mirabel88/ChiomaDevOpsLab.git'
    }

    stages {

        stage('Clone Repository on Master') {
            agent { label 'master' }
            steps {
                echo '🔄 Cloning ChiomaDevOpsLab repository on Master...'
                withCredentials([usernamePassword(credentialsId: 'github-pat', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                        git config --global user.email "chiomaobiekeh@gmail.com"
                        git config --global user.name "Chioma-Mirabel88"
                        rm -rf ChiomaDevOpsLab
                        git clone https://${USERNAME}:${PASSWORD}@github.com/Chioma-Mirabel88/ChiomaDevOpsLab.git
                    '''
                }
            }
        }

        stage('Compile on Slave1') {
            agent { label 'slave1' }
            steps {
                echo '⚙ Compiling the project on Slave1...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn compile -X'
                }
            }
        }

        stage('Code Review on Slave2') {
            agent { label 'slave2' }
            steps {
                echo '🔍 Running PMD analysis on Slave2...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn pmd:pmd -X'
                }
            }
        }

        stage('Unit Testing on Slave2') {
            agent { label 'slave2' }
            steps {
                echo '🧪 Running unit tests on Slave2...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn test -X'
                }
            }
        }

        stage('Package on Master') {
            agent { label 'master' }
            steps {
                echo '📦 Packaging the project on Master...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn package -X'
                }
            }
        }
    }
}
