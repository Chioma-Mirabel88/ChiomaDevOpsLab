pipeline {
    agent none

    tools {
        jdk 'chiomajava'
        maven 'chiomamaven'
    }

    stages {
        stage('Clone on Master') {
            agent { label 'master' }
            steps {
                echo 'Cloning source code on master...'
                checkout scm
            }
        }

        stage('Build on Master') {
            agent { label 'master' }
            steps {
                echo 'Building code on master...'
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Compile on Slave 1') {
            agent { label 'slave1' }
            steps {
                echo 'Compiling code on slave1...'
                sh 'mvn compile'
            }
        }

        stage('Review and Unit Test on Slave 2') {
            agent { label 'slave2' }
            steps {
                echo 'Code review and unit testing on slave2...'
                // Simulated review task
                echo 'Performing code review (simulated)...'
                
                // Run unit tests
                sh 'mvn test'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
