pipeline {
    agent any
    tools { 
        maven 'mvn' 
        jdk 'java' 
    }
   
    stages{
        stage ('CheckOut') {
            steps {
                 sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
                
               git 'https://github.com/jampani80/webApp.git'
               
            }
        }
        stage ('Build') {
            steps {
               
              
                sh "pwd"
                sh 'mvn package'
                
                
               
            }
        }
        
         stage ('Unit Test') {
            steps {
                
                echo "Running Unit test cases"
                sh 'mvn test'
                
            }
        }
        stage ('Code Scan') {
            steps {
                
                 echo "Running Static code analysis and security scans"
               
                
            }
        }
         stage ('Staging') {
            steps {
                
                sh 'cp /var/lib/jenkins/workspace/poc2/target/webApp.war /tmp/'
               
                
            }
        }
        stage ('Deploy') {
            steps {
                echo 'Deploying to DEV Server.'
                sh 'cp /tmp/webApp.war /usr/share/tomcat/webapps'
               
                
            }
        }
        
        stage ('Publish Report') {
            steps {   
        sh 'mkdir -p report'
        writeFile file: "target/integration-result.html",
                  text: buildHtmlReport(stageDefs)
        publishHTML([
                allowMissing         : false,
                alwaysLinkToLastBuild: true,
                keepAll              : true,
                reportDir            : 'target',
                reportFiles          : 'integration-result.html',
                reportName           : 'Integration result'])
    }
        } 
    }
}
