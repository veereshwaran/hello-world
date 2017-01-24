node {
   stage('Build') {
         git 'https://github.com/veereshwaran/hello-world-mvn.git/'
         sh "mvn install"
         archive 'target/*.jar'
   }

   stage('Publish') {
       freeStyleJob('NexusArtifactUploaderJob') {
    steps {
      nexusArtifactUploader {
        nexusVersion('nexus2')
        protocol('http')
        nexusUrl('i00039.hosts.appranix.info:8081/nexus')
        groupId('sp.sd')
        version('2.4')
        repository('releases')
        credentialsId('nexus')
        artifact {
            artifactId('nexus-artifact-uploader')
            type('jar')
            classifier('debug')
            file('nexus-artifact-uploader.jar')
        }
      }
    }
}
   }

   stage('Deploy to assembly') {
       echo 'Deploy to assembly'
   }

   stage('Deploy to ci') {
       echo 'Deploy to ci'
   }

   stage('Commit and Deploy to ci') {
       echo 'Commit and Deploy to ci'
   }
}
