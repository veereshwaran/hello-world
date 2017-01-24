node {
   stage('Build') {
         git 'https://github.com/veereshwaran/hello-world-mvn.git/'
         maven 'install'
         archive 'target/*.jar'
   }

   stage('Publish to nexus') {
      nexusArtifactUploader artifacts: [[
                                         artifactId: 'quick-demo-app', classifier: '',
                                         file: 'target/helloworld-1.0.3.war', type: 'war'
                                       ]],
         credentialsId: 'nexus',
         groupId: 'com.appranix',
         nexusUrl: 'i00039.hosts.appranix.info:8081/nexus',
         nexusVersion: 'nexus2',
         protocol: 'http',
         repository: 'releases',
         version: env.BUILD_ID
   }

   stage('Deploy to Prana') {
      withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'ci-appranix',
                            usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                //available as an env variable, but will be masked if you try to print it out any which way
                sh 'prana config set site=https://app.appranix.net/web/ -g'
                sh 'prana auth logout'
                sh "prana auth login --username=${env.USERNAME} --password=${env.PASSWORD} --account=devorg"
                sh "prana config set organization=devorg-veeresh -g"
                sh "prana config set assembly=demo -g"
                sh "prana design load design.yml"
                sh "prana design platform variable update -a demo -p helloworld appVersion=${env.BUILD_ID}"
                sh "prana design commit init-commit"
                sh "prana transition pull -e dev"
                sh "prana transition commit init-commit -e env"
                sh "prana transition deployment create -e dev"
            }
   }
}
