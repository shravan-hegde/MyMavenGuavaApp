pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/shravan-hegde/MyMavenGuavaApp.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Maven Project...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging JAR...'
                sh 'mvn package'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running Application...'
                
                // Try running if jar exists
                sh '''
                if ls target/*.jar 1> /dev/null 2>&1; then
                    java -cp target/*.jar com.example.App || echo "Main class not found"
                else
                    echo "No executable jar found"
                fi
                '''
            }
        }
    }

    post {
        success {
            echo 'Build Successful!'
        }
        failure {
            echo 'Build Failed!'
        }
    }
}
