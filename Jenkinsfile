pipeline {
    agent any
    
    tools {
        maven 'maven'
        jdk 'jdk'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository with personal access token
                git credentialsId: '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', url: 'https://github.com/shushinz/Web.git'
            }
        }
        
        stage('Test') {
            steps {
                // Execute JUnit test cases using Maven
                sh 'mvn test'
            }
        }
        
        stage('Build') {
            steps {
                // Compile the source code and package the application as war using Maven
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Archive the artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '744c54b6-cb91-40e5-85b3-dcdbfcdb6660', path: '', url: 'http://13.233.95.117:9090/')], contextPath: null, onFailure: false, war: '**/*.war'
            }
        }
    }
}
