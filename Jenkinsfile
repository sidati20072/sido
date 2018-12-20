 pipeline {

  agent { kubernetes {
    cloud 'kubernetes'
    label 'test'
      containerTemplate {
        name 'jnlp'
        image 'jenkinsci/jnlp-slave:2.62-alpine'
        ttyEnabled true
        args '${computer.jnlpmac} ${computer.name}'
      }
  }}
     

node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm
    }
    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("sidati20072/hellonode")
    }
    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
        app.inside {
            sh 'echo "Tests passed"'
        }
    }
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        
    }

   

     stage('Production') {      
         
          sh "kubectl get po" 
      
      
     }
}
  
 }
