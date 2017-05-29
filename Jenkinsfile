node('kube'){
stage 'Checkout'
    /* Checkout the code we are currently running against */
   checkout scm
 //  git url:'https://github.com/pingwin4ik/test_drupal.git'
  stage 'Build Docker image'
   sh 'docker build -t pingwin4ik/drupal .'
}
