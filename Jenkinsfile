node {
   stage('Build') {
         git 'https://github.com/veereshwaran/hello-world-mvn.git/'
         sh "mvn install"
         archive 'target/*.jar'
   }

   stage('Publish to nexus') {
      nexusArtifactUploader artifacts: [[artifactId: 'helloworld', classifier: '', file: 'target/helloworld-1.0.3.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.appranix', nexusUrl: 'i00039.hosts.appranix.info:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: '1.0.4'
   }

   stage('Deploy to assembly') {
       sh "prana"
       echo 'Deploy to assembly'
   }

   stage('Deploy to ci') {
       echo 'Deploy to ci'
   }

   stage('Commit and Deploy to ci') {
       echo 'Commit and Deploy to ci'
   }
}
