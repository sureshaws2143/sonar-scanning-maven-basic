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
  stage('SonarQube analysis') {
        if (env.BRANCH_NAME == 'master') {
        stage 'Only on master'
        println 'This happens only on master'
        } else {
        stage 'Other branches'
        println "Current branch ${env.BRANCH_NAME}"
        }
          withSonarQubeEnv(credentialsId: 'a6df94174c22090555ae29bfd03d0a9c2d69851e', installationName: 'Sonarqube') { // You can override the credential to be used
          //sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'

sh 'mvn sonar:sonar \
  -Dsonar.projectKey=sonarscanner-maven-basic \
  -Dsonar.host.url=http://10.1.3.30:9000 \
  -Dsonar.login=ba69203248ba92f48adb10d391deff03739d850f'

    }
  }
}