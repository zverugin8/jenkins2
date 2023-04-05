pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                withKubeConfig([credentialsId: 'dokub', serverUrl: 'https://kubernetes.docker.internal:6443']) {
                sh '''
                kubectl rollout status deploy hello-app
                kubectl get pods --selector=app=hello-app --output=jsonpath='{range .items[*]}{.metadata.name}{"\\n"}{end}' | xargs -I {} kubectl logs {}
                kubectl get svc hello-app-service
                '''
                } 
             }
         }
        stage('Deploy') {
            steps {
                withKubeConfig([credentialsId: 'dokub', serverUrl: 'https://kubernetes.docker.internal:6443']) {
                sh 'echo "Updating deploy"'
                sh 'kubectl apply -f hello-deploy.yaml'
                sh 'sleep 10'
                sh 'kubectl get pods -o wide'
                } 
             }
         }
        stage('Test') {
            steps {
                withKubeConfig([credentialsId: 'dokub', serverUrl: 'https://kubernetes.docker.internal:6443']) {
                sh '''
                echo "Testing access to service"
                PORT=$(kubectl get svc hello-app-service -o jsonpath={.spec.ports[0].nodePort})
                curl --fail --silent --show-error http://minikube:$PORT
                '''
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
}