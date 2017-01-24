node {
   stage('Build') {
         git 'https://github.com/veereshwaran/hello-world-mvn.git/'
         sh "mvn install"
         archive 'target/*.jar'
   }

   stage('Publish') {
       nexusArtifactUploader {
        nexusVersion('nexus2')
        protocol('http')
        nexusUrl('i00039.hosts.appranix.info:8081/nexus/')
        groupId('sp.sd')
        version('2.4')
        repository('releases')
        credentialsId('nexus')
        artifact {
            artifactId('hello')
            type('war')
            classifier('debug')
            file('target/helloworld-1.0.3.war')
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
