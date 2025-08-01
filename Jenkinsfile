pipeline {
    agent none

    tools {
        jdk 'chiomajava'
        maven 'chiomamaven'
    }

    environment {
        REPO_URL = 'https://github.com/Chioma-Mirabel88/ChiomaDevOpsLab.git'
    }

    stages {
        stage('Checkout') {
            agent any
            steps {
                echo '🔄 Cloning ChiomaDevOpsLab repository...'
                withCredentials([usernamePassword(
                    credentialsId: 'github-chioma',
                    usernameVariable: 'GIT_USERNAME',
                    passwordVariable: 'GIT_PASSWORD'
                )]) {
                    git url: "https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Chioma-Mirabel88/ChiomaDevOpsLab.git"
                }
            }
        }

        stage('Compile') {
            agent { label 'slave1' }
            steps {
                echo '⚙️ Compiling the Maven project on slave1...'
                sh 'mvn compile'
            }
        }

        stage('Code Review') {
            agent { label 'slave2' }
            steps {
                echo '🔍 Running static code analysis with PMD on slave2...'
                sh 'mvn pmd:pmd'
            }
        }

        stage('Test') {
            agent { label 'slave2' }
            steps {
                echo '🧪 Running tests on slave2...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            agent { label 'slave1' }
            steps {
                echo '📦 Packaging the application on slave1...'
                sh 'mvn package'
            }
        }
    }
}
