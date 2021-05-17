
 pipeline{
       agent { label 'master'} 
       stages {
          stage ("build") {
            steps {
                script {
                        docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub_id') {
                        FINAL_BRANCH = sh(returnStdout: true, script: 'echo ${BRANCH_NAME} | cut -d "/" -f2')
                        jobBaseName = sh(script: "echo ${BRANCH_NAME} | cut -d '/' -f2",returnStdout: true,)
                        sh "env" 
                        def customImage = docker.build("manibpl0509/release", "-f Dockerfile .")
                        /* Push the container to the custom Registry */
                        customImage.push("${env.BUILD_NUMBER}")
                       }
                   }
              }
          }
       }
 }
