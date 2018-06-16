pipeline {
    agent any
    
    parameters { 
         string(name: 'tomcat', defaultValue: '167.99.199.137', description: 'Staging Server')
         string(name: 'tomcat-prod', defaultValue: '167.99.199.137', description: 'Production Server')
    } 
 
    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }
 
stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
 
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "scp -r **/target/*.war root@${params.tomcat}:/usr/share/tomcat/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "scp -r **/target/*.war root@${params.tomcat}:/usr/share/tomcat-prod/webapps"
                    }
                }
            }
        }
    }
}
