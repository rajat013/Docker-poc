pipeline {
environment {
// registry = "https://hub.docker.com/repository/docker/rajat013/test"
// registryCredential = 'dockerhub_cred'
// dockerImage = ''
//
   app= ''
}
agent any
stages {
stage('Building our image') {
steps{
script {
app = docker.build("rajat013/test")
}
}
}
stage('Deploy our image') {
   when {
      expression {
      
         return ${params.PUSH_IMAGE}
      }
   }
steps{
script {
docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_cred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}
