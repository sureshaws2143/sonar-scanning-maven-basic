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
          withSonarQubeEnv(credentialsId: '3eb0086801b129b5036cdfa9122cf130fc1f6ad7', installationName: 'Sonarqube') { // You can override the credential to be used
          //sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'

// sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=sonarscanner-maven-basic \
//   -Dsonar.host.url=http://10.1.3.29:9000/sonarqube \
//   -Dsonar.login=5d7694152e415c79121e161e461066048016117d'

sh 'mvn sonar:sonar \
  -Dsonar.projectKey=sonarscanner-maven-basic \
  -Dsonar.host.url=http://10.1.3.29:9000/sonarqube \
  -Dsonar.login=5d7694152e415c79121e161e461066048016117d'

    }
  }
}