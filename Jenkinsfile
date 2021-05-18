 pipeline{
       agent { label 'master'} 
       stages {
          stage ("build") {
            steps {
                script {
                        docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub_id') {
                        FINAL_BRANCH = sh(returnStdout: true, script: 'echo ${BRANCH_NAME} | cut -d "/" -f2')
                        FINAL_TAG = sh(returnStdout: true, script: 'echo ${BUILD_NUMBER} | cut -d "/" -f1')
                        sh "echo $FINAL_BRANCH"
                        sh "echo $FINAL_TAG"
                        sh "echo $BUILD_NUMBER"
                        sh "echo $FINAL_BRANCH"
                         def customImage = docker.build("manibpl0509/release-test:'$FINAL_BRANCH-$FINAL_TAG'", "-f Dockerfile .")
                        /* Push the container to the custom Registry */
                         customImage.push()
                       }
                 }
              }
          }
       }
 }
