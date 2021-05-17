
 pipeline{
       agent { label 'master'} 
       stages {
          stage ("build") {
            steps {
                script {
          docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub_id') {
          sh "pwd"
          def customImage = docker.build("manibpl0509/${env.GIT_BRANCH}-${env.BUILD_NUMBER}", "-f Dockerfile .")
          /* Push the container to the custom Registry */
          customImage.push("${env.BUILD_NUMBER}")
         }
        }
        }
          }
       }
 }
