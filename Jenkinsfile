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
        stage('Deploy Frontend'){
            steps{
                dir('frontend'){
                    git 'https://github.com/rgosm/tasks-frontend'
                    bat 'mvn clean package'
                    deploy adapters: [tomcat8(credentialsId: 'user_tomcat', 
                    path: '', 
                    url: 'http://localhost:8090')], 
                    contextPath: 'tasks', 
                    war: 'target/tasks.war'
                }

            }
        }
        stage('Functional Test'){
            steps{
                dir('functional-test'){
                    git branch: 'main', url: 'https://github.com/rgosm/tasks-functional-test'
                    bat 'mvn test'
                }
            }
        }
    }
}