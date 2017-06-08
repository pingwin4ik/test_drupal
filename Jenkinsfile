/Lets define a unique label for this build.
def label = "buildpod.${env.JOB_NAME}.${env.BUILD_NUMBER}".replace('-', '_').replace('/', '_')

//Lets create a new pod template with jnlp and maven containers, that uses that label.
podTemplate(label: label, containers: [
        containerTemplate(name: 'dind', image: 'docker:stable-dind', ttyEnabled: true, privileged: true, envVars: [ containerEnvVar(key: 'DOCKER_DRIVER', value: 'overlay'),]),
        containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:latest', ttyEnabled: true, command: 'cat')
        ],

        ) {

    //Lets use pod template (refernce by label)
    node(label) {
            stage('Run Command') {
                    container(name: 'dind') {
                       // sh 'docker info'
                        git 'https://github.com/pingwin4ik/test_drupal.git'
                        sh("docker build  -t pingwin4ik/drupal:${BUILD_NUMBER} .")
                        withDockerRegistry([credentialsId: '81ec2bf1-1752-48cc-8c79-d81e6a7535b6']) {
                        sh("docker push pingwin4ik/drupal:${BUILD_NUMBER}")}
                      }
                    }
            stage('deploy') {
     container(name:'kubectl') {
         // sh "kubectl get nodes"
         sh "kubectl apply -f depl.yaml"
        sh "kubectl set image deployment drupal drupal=pingwin4ik/drupal:${BUILD_NUMBER}"
      }
                        }
                        }
}
