node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       app = docker.build("drsezginerdem/test-gitops")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }
    // stage('Docker Login') {
  

    //     app.inside {
    //         sh 'docker login -u drsezginerdem -p 2283156473'
    //     }
    // }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'sezgin_dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    // stage('Trigger ManifestUpdate') {
    //             echo "triggering test-gitops-updatemanifest job"
    //             build job: 'test-gitops-updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    //     }
}
