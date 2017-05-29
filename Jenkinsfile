node('kube'){
stage 'Checkout'
    /* Checkout the code we are currently running against */
   checkout scm
 //  git url:'https://github.com/pingwin4ik/test_drupal.git'
  stage 'Build Docker image'
   def pingwin = docker.build('pingwin4ik/drupal', '--no-cache=true .')
}
