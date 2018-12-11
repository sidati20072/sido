node {
    def app

   

     stage('Production') {
      withKubeConfig([credentialsId: 'sshkubernetes', serverUrl: 'https://192.168.99.100:8443']) {
      
       sh 'kubectl run --image=sidati20072/hellonode '

       
      }
     }
}
