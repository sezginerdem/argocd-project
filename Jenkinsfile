node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       app = docker.build("sezginerdem/test")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        // This step should not normally be used in your script. Consult the inline help for details.
withDockerRegistry(credentialsId: 'sezgin_dockerhub', url: 'https://hub.docker.com/') {
    // some block
} {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering test-gitops-updatemanifest job"
                build job: 'test-gitops-updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
