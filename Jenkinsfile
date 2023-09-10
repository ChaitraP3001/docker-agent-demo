pipeline {
    
   agent any

    tools {
      maven 'maven3'
    }
    
    
    stages{
        stage ('Checkout') {
            steps{
                checkout poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ChaitraP3001/docker-agent-demo.git']])
            }
            
        }
        stage ('Build') {
            agent{
                label "sshagent1"
            }
            steps {
                echo "Build Stage is in progress"
                sh 'mvn compile'
            }
            
        }
        stage ('Test'){
            agent{
                label "sshagent1"
            }
            steps {
                echo "Test Stage is in progress"
                sh 'mvn test'
            }
            
        }
         stage('Deploy'){
             agent{
                label "sshagent2"
            }
            input {
              message 'Do you want to deploy build?'
              ok 'Yes I want'
              parameters {
                string description: 'Who is Approver?', name: 'Approver'
              }
            }
            steps{
                echo 'Deploying Build'
            }
        }
    
    }
}
