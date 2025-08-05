pipeline {
    agent any

    tools {
        jdk 'chiomajava'
        maven 'chiomamaven'
    }

    environment {
        REPO_URL = 'https://github.com/Chioma-Mirabel88/ChiomaDevOpsLab.git'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '🔄 Cloning ChiomaDevOpsLab repository using GitHub username and PAT...'
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

        stage('Compile') {
            steps {
                echo '⚙️ Compiling the Maven project with debug info...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn compile -X'
                }
            }
        }

        stage('Code Review') {
            steps {
                echo '🔍 Running static code analysis with PMD...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn pmd:pmd -X'
                }
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn test -X'
                }
            }
        }

        stage('Package') {
            steps {
                echo '📦 Packaging the application...'
                dir('ChiomaDevOpsLab') {
                    sh 'mvn package -X'
                }
            }
        }
    }
}

