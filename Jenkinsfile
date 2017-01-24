node {
   stage('Build') {
         git 'https://github.com/veereshwaran/hello-world-mvn.git/'
         maven 'install'
         archive 'target/*.jar'
   }

   stage('Publish to nexus') {
      nexusArtifactUploader artifacts: [[
                                         artifactId: 'helloworld', classifier: '', 
                                         file: 'target/helloworld-1.0.3.war', type: 'war'
                                       ]], 
         credentialsId: 'nexus', 
         groupId: 'gowtham.appranix', 
         nexusUrl: 'i00039.hosts.appranix.info:8081/nexus', 
         nexusVersion: 'nexus2', 
         protocol: 'http', 
         repository: 'releases', 
         version: '1.0.6'
   }

   stage('Deploy to assembly') {
      withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'ci-appranix',
                            usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                //available as an env variable, but will be masked if you try to print it out any which way
                sh 'echo $PASSWORD'
                echo "${env.USERNAME}"
                sh 'prana auth login --username=$USERNAME --password=$PASSWORD --account=devorg'
            }
       echo 'Deploy to assembly'
   }

   stage('Deploy to ci') {
       echo 'Deploy to ci'
   }

   stage('Commit and Deploy to ci') {
       echo 'Commit and Deploy to ci'
   }
}
