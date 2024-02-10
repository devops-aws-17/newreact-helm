pipeline{
  agent any
  stages{
    stage('connecting to cluster'){
      steps{
      sh 'kubectl config use-context arn:aws:eks:us-west-2:897276212041:cluster/devops-eks-gCFGYxzJ'
      }
  }
    stage('create frontend namespace'){
      steps{
    sh '''
        myNamespace="frontend"
       kubectl get namespace | grep -q "^$myNamespace " || kubectl create namespace $myNamespace
         '''
    }
    }
  stage('deploy reactjs'){
    steps{
    sh 'helm upgrade --install devops-frontend $WORKSPACE --values $WORKSPACE/frontend-values.yaml --namespace frontend '
    }
  }
 stage('pod status'){
   steps{
   sh 'kubectl get pods -n frontend'
   }
 }
    
}
post {
   always{
    cleanWs()
   }
}
}
