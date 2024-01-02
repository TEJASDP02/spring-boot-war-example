pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
            
                sh "mvn test"
                slackSend channel: 'jenkins', message: 'job started'
            }
            
        }   
        stage("Build"){
            steps{
                sh "mvn package"
                slackSend channel: 'jenkins', message: 'building'
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container 
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://192.168.1.55:8082')], contextPath: '/app', war: '**/*.war'
                slackSend channel: 'jenkins', message: 'deployed to test server'
            }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container 
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.233.157.129:8081')], contextPath: '/app', war: '**/*.war'
                slackSend channel: 'jenkins', message: 'deployed to prod server'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            slackSend channel: 'jenkins', message: 'success'
           
        }
        failure{
            echo "========pipeline execution failed========"
            slackSend channel: 'jenkins', message: 'failure'
        }
    }
}
