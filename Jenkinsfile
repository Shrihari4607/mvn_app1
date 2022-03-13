pipeline {
    agent any
    
    tools {
         maven 'maven'
    }
    
    stages {
      //stage('Scm') {
          //  steps {
              // checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Shrihari4607/mvn_app1.git']]])
           // }
        //}
        // webhook test
        stage('Build') {
            steps {
                bat """mvn -B -DskipTests clean package"""
            }
        }
        stage('Test') {
            steps {
                bat """mvn test"""
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Artifact-Upload') {
            steps {
                echo "uploading ${app_name}-1.0.${BUILD_Number}.zip to Nexus"
            }
        }
    }
    post {
        always{
           // emailext ( body: 'test', subject: '', 
                      //to: 'shrihari4607@gmail.com')
            
            //env.ForEmailPlugin = env.WORKSPACE      
            emailext body: '''${SCRIPT, template="email_html.template"}''', 
            subject: currentBuild.currentResult + " : " + env.JOB_NAME, 
            to: 'shrihari4607@gmail.com'
        }
    }
}
