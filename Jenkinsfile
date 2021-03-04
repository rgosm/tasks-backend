pipeline{
    agent any

    stages{
        stage('Build Backend'){
            steps{
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage('Deploy Backend'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'user_tomcat', 
                path: '', 
                url: 'http://localhost:8090')], 
                contextPath: 'tasks-backend', 
                war: 'target/tasks-backend.war'
            }
        }
    }
}