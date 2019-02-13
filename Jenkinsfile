pipeline {
    agent any
    tools { 
        maven 'mvn' 
        jdk 'java' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }

        stage ('CheckOut') {
            steps {
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
        
        stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
                    agent {
                        label "windows"
                    }
                    steps {
                        bat "run-tests.bat"
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
                }
                stage('Test On Linux') {
                    agent {
                        label "linux"
                    }
                    steps {
                        sh "run-tests.sh"
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
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
    }
}
