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
          withSonarQubeEnv(credentialsId: '199c1a35-7206-4170-89c1-0ea5d2910d02', installationName: 'Sonarqube') { // You can override the credential to be used
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
    }
  }
}