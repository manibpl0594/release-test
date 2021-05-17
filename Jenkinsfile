
 pipeline{
       agent { label 'master'} 
       stages {
          stage ("build") {
            steps {
                script {
                        docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub_id') {
                        echo $BRANCH_NAME
                        FINAL_BRANCH = sh(returnStdout: true, script: 'echo ${BRANCH_NAME} | cut -d "/" -f2')
                        jobBaseName = sh(script: "echo ${BRANCH_NAME} | cut -d '/' -f2", returnStdout: true,)
                        echo $FINAL_BRANCH
                        echo $jobBaseName
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
