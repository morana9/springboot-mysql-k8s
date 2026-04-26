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
                sh 'chmod +x mvnw'
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Upload to Nexus') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'nexus-creds',
                    usernameVariable: 'NEXUS_USER',
                    passwordVariable: 'NEXUS_PASS'
                )]) {

                    sh '''
                    curl -v -u $NEXUS_USER:$NEXUS_PASS \
                    --upload-file target/*.jar \
                    http://192.168.49.2:30081/repository/maven-releases/springboot-app.jar
                    '''
                }
            }
        }
    }
}

