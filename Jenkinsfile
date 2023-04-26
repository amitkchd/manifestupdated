node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'amitkchd', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email mynavitaire@gmail.com"
                        sh "git config user.name rakhar"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+mynav1234/test.*+mynav1234/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        //sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/GitOpskubernetesmanifestRakhi.git HEAD:main"
                        sh "minikube kubectl -- apply -f deployment.yaml"
      }
    }
  }
}
}
