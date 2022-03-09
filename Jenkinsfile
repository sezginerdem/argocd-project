node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
  
       app = docker.build("drsezginerdem/test-gitops")
    }

    stage('Test image') {
        script
        //app.inside 
        {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'sezgin_dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                //build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}





// node {
//     def app

//     stage('Clone repository') {
//         checkout scm
//     }

//     stage('Build image') {
//        app = docker.build("drsezginerdem/test-gitops:latest")
//     }

//     // stage('Test image') {
//     //     app.inside {
//     //         sh 'echo "Tests passed"'
//     //     }
//     // }

//     stage('Push image to DockerHub') {
        
//         docker.withRegistry('https://registry.hub.docker.com', 'sezgin_dockerhub') {
//             app.push("${env.BUILD_NUMBER}")
//         }
//     }
    
//     stage('Update GitHub Repository') {
//             script {
//                 catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
//                     withCredentials([usernamePassword(credentialsId: 'sezgin_github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
//                         //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
//                         sh "git config user.email drsezginerdem@gmail.com"
//                         sh "git config user.name sezginerdem"
//                         //sh "git switch master"
//                         sh "cat deployment.yaml"
//                         sh "sed -i 's+drsezginerdem/test-gitops.*+drsezginerdem/test-gitops:${env.BUILD_NUMBER}+g' deployment.yaml"
//                         sh "cat deployment.yaml"
//                         sh "git add ."
//                         sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
//                         sh "git push -f https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-project.git HEAD:main"
//       }
//     }
//   }
// }
// }
