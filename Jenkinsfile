pipeline {
    agent any
    tools { 
        maven 'mvn' 
        jdk 'java' 
             
    }
   
    stages{
        
        stage ('Build') {
            steps {
                echo "****************************CheckOut & Build Process Started***************"
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
                 git 'https://github.com/jampani80/webApp.git'
                echo "****************************CheckOut Completed and Build started***************"
                sh "pwd"
                sh 'mvn package'
                 echo "****************************Build Completed***************"
            }
        }
        parallel {
         stage ('Unit Test') {
            steps {
                
                echo "****************Running Unit test cases*************"
                sh 'mvn test'
                 echo "****************Completed Unit test cases*************"
            }
        }
        stage ('Code Scan') {
            steps {
                
                 echo "Running Static code analysis and security scans"
               
                
            }
        }
        }
         stage ('Staging') {
            steps {
                 echo "*************Staging deployable artifacts****************************"
                sh 'cp /var/lib/jenkins/workspace/poc2/target/webApp.war /tmp/'
               
                
            }
        }
        stage ('Deploy') {
            steps {
                echo '******************Deploying to DEV Server.*******************'
                sh 'cp /tmp/webApp.war /usr/share/tomcat/webapps'
               
                
            }
        }
        

    }
}
