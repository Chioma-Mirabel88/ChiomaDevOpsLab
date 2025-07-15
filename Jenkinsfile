pipeline {
    agent any

    tools {
        jdk 'ChiomaJava'
        maven 'ChiomaMaven'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git 'https://github.com/Chioma-Mirabel88/ChiomaDevOpsLab.git'
            }
        }

        stage('Compile with Maven') {
            steps {
                sh 'mvn clean compile'
            }
        }
    }
}

