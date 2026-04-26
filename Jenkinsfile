pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/morana9/springboot-mysql-k8s.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Upload to Nexus') {
            steps {
                sh '''
                curl -v -u admin:admin123 --upload-file target/*.jar \
                http://nexus-service:8081/repository/maven-releases/com/example/springboot-app/1.0/springboot-app-1.0.jar
                '''
            }
        }
    }
}

