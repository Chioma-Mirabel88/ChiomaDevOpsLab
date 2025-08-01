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
                withCredentials([string(credentialsId: 'github-pat', variable: 'GITHUB_PAT')]) {
                    git url: "https://${GITHUB_PAT}@github.com/Chioma-Mirabel88/ChiomaDevOpsLab.git"
                }
            }
        }

        stage('Compile') {
            agent { label 'slave1' }
            steps {
                echo '⚙️ Compiling the Maven project on slave1 with debug info...'
                sh 'mvn compile -X'
            }
        }

        stage('Code Review') {
            agent { label 'slave2' }
            steps {
                echo '🔍 Running static code analysis with PMD on slave2 with debug info...'
                sh 'mvn pmd:pmd -X'
            }
        }

        stage('Test') {
            agent { label 'slave2' }
            steps {
                echo '🧪 Running tests on slave2 with debug info...'
                sh 'mvn test -X'
            }
        }

        stage('Package') {
            agent { label 'master' }
            steps {
                echo '📦 Packaging the application on master with debug info...'
                sh 'mvn package -X'
            }
        }
    }
}
