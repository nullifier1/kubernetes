node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh 'export CONTAINER_NUMBER=$(cat /home/number)'
                        sh "git config user.email infinityofcore@gmail.com"
                        sh "git config user.name nullifier1"
                        //sh "git switch master"
                        sh "cat gogs-deployment.yaml"
                        sh "sed -i 's+infinityofcore/testgogs.*+infinityofcore/testgogs:$CONTAINER_NUMBER+g' gogs-deployment.yaml"
                        sh "cat gogs-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: $CONTAINER_NUMBER'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetes.git HEAD:main"
      }
    }
  }
}
}
