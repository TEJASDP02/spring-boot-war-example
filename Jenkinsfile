pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
            
                sh "mvn test"
               
            }
            
        }   
        stage("Build"){
            steps{
                sh "mvn package"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container 
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://192.168.1.55:8082')], contextPath: '/app', war: '**/*.war'
              
            }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container 
                echo "prod"

            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
           
        }
        failure{
            echo "========pipeline execution failed========"
            
        }
    }
}
