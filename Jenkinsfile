// stage 'Init'
// node {
//   checkout scm
//   sh 'echo $BRANCH_NAME'
// }
// if (env.BRANCH_NAME == 'master') {
//   stage 'Only on master'
//   println 'This happens only on master'
// } else {
//   stage 'Other branches'
//   println "Current branch ${env.BRANCH_NAME}"
// }

node {
stage ('Init'){
  checkout scm
  sh 'echo $BRANCH_NAME'
}
  stage('SCM') {
    git 'https://github.com/sureshaws2143/sonar-scanning-maven-basic.git'
  }
    stage('Build') {
    sh 'mvn -v'
    //git 'https://github.com/sureshaws2143/sonar-scanning-maven-basic.git'
  }
  stage('SonarQube analysis') {
        if (env.BRANCH_NAME == 'master') {
        stage 'Only on master'
        println 'This happens only on master'
        } else {
        stage 'Other branches'
        println "Current branch ${env.BRANCH_NAME}"
        }
          withSonarQubeEnv(credentialsId: 'jenkins-sonar-int', installationName: 'sonarqube') { // You can override the credential to be used
          //sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'

// sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=sonarscanner-maven-basic \
//   -Dsonar.host.url=http://10.1.3.29:9000/sonarqube \
//   -Dsonar.login=5d7694152e415c79121e161e461066048016117d'

// sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=sonarscanner-maven-basic \
//   -Dsonar.host.url=http://10.1.3.29:9000/sonarqube \
//   -Dsonar.login=1141d5896f177861ef5b06bd7fcde2e555fd6e80'

sh 'mvn sonar:sonar \
  -Dsonar.projectKey=sonar-scanning-maven-basic \
  -Dsonar.host.url=http://192.168.1.114:9000 \
  -Dsonar.login=b59ec99b58eed86f236c8173a3164a96e6d0eb73'

    }
// emailext(
//   to : 'suresh.profile2008@gmail.com;bhupathireddys@gmail.com;nagas400@gmail.com'
//   subject : "Jenkins JOB Status '${env.JOB_BASE_NAME} [${env.BUILDID}]'",
//   mimeType: 'text/html',
//   body: """ Hi All, <div>The Jenkis Build is <span style='color:red'><b> .....</b></span></div>
//   <div><b> JENKINS URL: </b><a href='${env.BUILD_URL}'>${env.BUILD_URL}</a>""",
//   <p><b>SONAR ANALYSIS: </b><a href=http://10.1.3.29:9000/sonarqube/dashboard?id=sonarscanner-maven-basic>http://10.1.3.29:9000/sonarqube/dashboard?id=sonarscanner-maven-basic </a><p></div>
//   recipientProviders: [[$class: 'DevelopersReciptientProvider']]
// )


  }
}