node {
    def app

   

     stage('Production') {
      withKubeConfig([credentialsId: 'sshkubernetes', serverUrl: 'https://192.168.99.100:8443']) {
      
       sh 'kubectl create cm nodejs-app --image=sidati20072/hellonode  -o=yaml --dry-run > deploy/cm.yaml'

        sh 'kubectl apply -f deploy/ '
      }
     }
}
