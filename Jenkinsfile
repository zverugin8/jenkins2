pipeline {
    agent any
    environment{
      CLOUDSDK_CORE_PROJECT='saroka-gc-bootcamp'
      CLIENT_EMAIL='saroka-lab-02@saroka-gc-bootcamp.iam.gserviceaccount.com'
    }
    stages {
        stage('Test') {
            steps {
                withKubeConfig([credentialsId: 'kubecred', serverUrl: 'https://192.168.58.2:8443']) {
                sh 'ls -al'
                sh 'kubectl apply -f hello-deploy.yaml'
                sh 'kubectl get pods' 
                } 
             }
         }
// post {
//   always {
//   sh '''
//     PATH=/gcloud/google-cloud-sdk/bin:$PATH
//     gcloud auth revoke $CLIENT_EMAIL
//   '''
//   }
// }
}
