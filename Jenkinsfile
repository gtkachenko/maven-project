
pipeline {
   /* A declareative Pipeline */
   agent any
   stages{
       stage('Build'){
           steps {
               sh 'mvn clean package'
           }
           post {
               success {
                   echo 'Now Archiving ...'
                   archiveArtifacts artifacts: '**/target/*.war'
               }
           }
       }
       stage ('Deploy Staging'){
           steps {
               build job: 'deploy-to-stageing'
           }
       }
      
       stage ('Deploy to Production'){
           steps{
               timeout(time:5, unit:'DAYS'){
                   input message:'Approve PRODUCTION Deployment?'
               }
	       
               build job: 'deploy-to-prod'
           }
           post {
               success {
                   echo 'Code deployed to Production.'
               }
               
               failure {
                   echo 'Deployment failed.'
               }
           }
       }
      
    }	
}
