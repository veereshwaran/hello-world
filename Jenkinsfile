node {
   stage('Build') {
         git 'https://github.com/veereshwaran/hello-world-mvn.git/'
         sh "mvn install"
   }

   stage('Push to nexus') {
       echo 'push to nexus'
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
