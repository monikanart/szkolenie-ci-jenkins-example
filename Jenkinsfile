pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3"
        jdk "jdk-17"
    }

    stages {
        stage('Clean') {
            steps {
               cleanWs()
            }
        }
        
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/spring-projects/spring-petclinic'
                sh 'mvn clean verify'
            }
        }
    }
    
    post {
        always {
            junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
        }
        success {
            slackSend  channel: "#jenkins-monika-nartowska", message: "Build success ${env.BUILD_TAG} ${env.BUILD_URL}"
        }
        failure {
            slackSend   channel: "#jenkins-monika-nartowska", message: "Failure success"
        }
        unstable {
            slackSend channel: "#jenkins-monika-nartowska", message: "Unstable success"
        }
    }
}
