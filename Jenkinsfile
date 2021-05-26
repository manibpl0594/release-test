 pipeline{
       agent { label 'master'} 
       stages {
          stage ("build") {
            steps {
                script {
                        docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub_id') {
                        FINAL_BRANCH = sh(returnStdout: true, script: 'echo ${BRANCH_NAME} | cut -d "/" -f2 | tr -d "[:space:]"')
                        FINAL_TAG = sh(returnStdout: true, script: 'echo ${BUILD_NUMBER} | tr -d "[:space:]"')
                        sh "echo $FINAL_BRANCH"
                        sh "echo $FINAL_TAG"
                        sh "echo $FINAL_BRANCH-$FINAL_TAG" 
                         def customImage = docker.build("manibpl0509/release-'$FINAL_BRANCH':'$FINAL_TAG'", "-f Dockerfile .")
                        /* Push the container to the custom Registry */
                         customImage.push()
                       }
                 }
              }
          }
       }
 }
