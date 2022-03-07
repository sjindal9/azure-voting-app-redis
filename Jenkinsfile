pipeline {
   agent any

   stages {
      stage('Branch Name') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            sh 'docker images -a'
            sh """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """
         }
      }
      stage('Start the App'){
       when{branch 'master'}
         steps{
            echo "Starting the app.."
         }
         post{
            success{
               echo "Application started sucessfully"
            }
            failure{
               echo "Application failed to start"
            }
         }
      }
      stage("Stope the App"){
         steps{
            echo "stoping the app..."
            //sh 'docker compose down'
            sh 'docker container stop jenkins-pipeline'
         }
      }
   }
      
}