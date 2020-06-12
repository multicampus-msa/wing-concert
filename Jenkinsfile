node {
     stage('Clone repository') {
         checkout scm
     }
     stage('chmod') {
         sh 'chmod +x gradlew'
     }
     stage('Gradle Build') {
         sh './gradlew bootjar'
         sh 'cp /var/lib/jenkins/workspace/wing-concert/build/libs/*.jar ./'
     }
     stage('Build & Push image') {
          docker.withRegistry('https://registry.hub.docker.com', 'dleogml-docker') {
             def image = docker.build("dleogml/wing-concert:latest")
             image.push()
             sh 'sudo docker service update --image dleogml/wing-concert wing-concert'
         }
     }
 }