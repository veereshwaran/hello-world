node {
   stage('Build') {
        if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' install"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
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
