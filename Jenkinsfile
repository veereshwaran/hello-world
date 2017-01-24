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
      withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'ci-appranix112',
                            usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                //available as an env variable, but will be masked if you try to print it out any which way
                sh 'echo $PASSWORD'
                echo "${env.USERNAME}"
                sh 'pwd'
                sh 'prana config set site=https://app.appranix.net/web/ -g'
                sh 'prana auth logout'
                sh "prana auth login --username=${env.USERNAME} --password=${env.PASSWORD} --account=devorg"
                sh "prana config set organization=devorg-veeresh -g"
                sh "prana config set assembly=test -g"
                sh "prana design load design.yml"
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
