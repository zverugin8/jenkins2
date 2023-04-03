pipeline {
    agent any
    environment{
      CLOUDSDK_CORE_PROJECT='saroka-gc-bootcamp'
      CLIENT_EMAIL='saroka-lab-02@saroka-gc-bootcamp.iam.gserviceaccount.com'
    }
    stages {
        stage('Test') {
            steps {
                // withCredentials([file(credentialsId: 'gclous-sa-02', variable: 'GCLOUD_CREDS')]) {
                //   sh '''
                //   PATH=/gcloud/google-cloud-sdk/bin:$PATH
                //   gcloud version
                //   gcloud auth activate-service-account  --key-file=$GCLOUD_CREDS
                //   echo gcloud compute zones list
                //   '''                 
                // }
                withKubeConfig([credentialsId: 'kubecred', serverUrl: 'https://192.168.58.2:55566']) {
                sh 'kubectl get pods'
                }
            } 
    }
}
post {
  always {
  // sh '''
  //   PATH=/gcloud/google-cloud-sdk/bin:$PATH
  //   gcloud auth revoke $CLIENT_EMAIL
  // '''
  }
}
}
