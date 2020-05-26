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

node ('dev-agentnode')
  {
stage ('Init'){
  // checkout scm
  // sh 'echo $BRANCH_NAME'
}

stage ('Clean Workspace'){
  // checkout scm
  step([$class: 'WsCleanup'])
  sh 'echo $BRANCH_NAME'
}

  stage('Prepare Workspace') {
    git 'https://github.com/sureshaws2143/sonar-scanning-maven-basic.git'
    println "Current branch ${env.BRANCH_NAME}"
    sh 'echo $BRANCH_NAME'
  }

  stage('SonarQube analysis') {
        // if (env.BRANCH_NAME == 'master') {
        // stage 'Only on master'
        // println 'This happens only on master'
        // } else {
        // stage 'Other branches'
        // println "Current branch ${env.BRANCH_NAME}"
        // }
          //withSonarQubeEnv(credentialsId: 'jenkins-sonar-int', installationName: 'sonarqube') { // You can override the credential to be used
          //sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'

// sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=sonarscanner-maven-basic \
//   -Dsonar.host.url=http://10.1.3.29:9000/sonarqube \
//   -Dsonar.login=5d7694152e415c79121e161e461066048016117d'

// sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=sonarscanner-maven-basic \
//   -Dsonar.host.url=http://10.1.3.29:9000/sonarqube \
//   -Dsonar.login=1141d5896f177861ef5b06bd7fcde2e555fd6e80'

// sh 'mvn -Dmaven.test.skip=true clean install sonar:sonar \
//   -Dsonar.projectKey=sonar-scanning-maven-basic \
//   -Dsonar.host.url=http://192.168.1.114:9000 \
//   -Dsonar.login=b59ec99b58eed86f236c8173a3164a96e6d0eb73'

// sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=sonar-scanning-maven-basic \
//   -Dsonar.host.url=http://192.168.1.114:9000 \
//   -Dsonar.login=b59ec99b58eed86f236c8173a3164a96e6d0eb73'

    //}
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

    stage('App Build') {
    sh 'mvn clean install -Dmaven.test.skip=true'
    }

// Artifactory Upload Stage -- New



// stage("publish to nexus") 
// {
//         nexusArtifactUploader(
//             nexusVersion: 'nexus3',
//             protocol: 'http',
//             nexusUrl: '192.168.1.160:8090',
//             groupId: 'org.sonarqube',
//             version: '1.0',
//             repository: 'maven-releases',
//             credentialsId: 'nexus',
//             artifacts: [
//                 [artifactId: 'sonarscanner-maven-basic',
//                 classifier: '',
//                 file: 'sonarscanner-maven-basic-' + '$version' + '.jar',
//                 type: 'jar']
//             ]
//         )
// }

// stage("publish to nexus") 
// {
// //nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/sonarscanner-maven-basic-1.0-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'sonarscanner-maven-basic', groupId: 'org.sonarqube', packaging: 'jar', version: '1.0']]]
// nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/sonarscanner-maven-basic-1.0-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'sonarscanner-maven-basic', groupId: 'org.sonarqube', packaging: 'jar', version: '1.0']]]
// }

// stage("publish to nexus") 
// {
// nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/sonarscanner-maven-basic-1.0-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'sonarscanner-maven-basic', groupId: 'org.sonarqube', packaging: 'jar', version: '1.0']]]
// }

stage("publish to nexus") 
{
  //createTag nexusInstanceId: 'nexus', tagName: '${env.BUILD_NUMBER}'
  nexusArtifactUploader artifacts: [[artifactId: 'sonarscanner-maven-basic', classifier: '', file: 'sonarscanner-maven-basic-1.0-SNAPSHOT.jar', type: 'jar']], credentialsId: '', groupId: 'org.sonarqube', nexusUrl: '192.168.1.160:8090', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '1.0'
//  nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/sonarscanner-maven-basic-1.0-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'sonarscanner-maven-basic', groupId: 'org.sonarqube', packaging: 'jar', version: '1.0']]]
}

        // stage("publish to nexus") 
        // {
        //             // Read POM xml file using 'readMavenPom' step , this step 'readMavenPom' is included in: https://plugins.jenkins.io/pipeline-utility-steps
        //             pom = readMavenPom file: "pom.xml";
        //             // Find built artifact under target folder
        //             filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
        //             // Print some info from the artifact found
        //             echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
        //             // Extract the path from the File found
        //             artifactPath = filesByGlob[0].path;
        //             // Assign to a boolean response verifying If the artifact name exists
        //             artifactExists = fileExists artifactPath;
        //             if(artifactExists) {
        //                 echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
        //                 nexusArtifactUploader(
        //                     nexusVersion: NEXUS_VERSION,
        //                     protocol: NEXUS_PROTOCOL,
        //                     nexusUrl: NEXUS_URL,
        //                     groupId: pom.groupId,
        //                     version: pom.version,
        //                     repository: NEXUS_REPOSITORY,
        //                     credentialsId: NEXUS_CREDENTIAL_ID,
        //                     artifacts: [
        //                         // Artifact generated such as .jar, .ear and .war files.
        //                         [artifactId: pom.artifactId,
        //                         classifier: '',
        //                         file: artifactPath,
        //                         type: pom.packaging],
        //                         // Lets upload the pom.xml file for additional information for Transitive dependencies
        //                         [artifactId: pom.artifactId,
        //                         classifier: '',
        //                         file: "pom.xml",
        //                         type: "pom"]
        //                     ]
        //                 );
        //             } else {
        //                 error "*** File: ${artifactPath}, could not be found";
        //             }
        //         }


// stage("publish to nexus") 
// {
//   // def server = Artifactory.server "artifactory@ibsrv02"
//   def server = Artifactory.server "artifactory"
//   def buildInfo = Artifactory.newBuildInfo()
//   buildInfo.env.capture = true
//   def rtMaven = Artifactory.newMavenBuild()
//   // rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
//   // rtMaven.opts = "-Denv=dev"
//   // rtMaven.deployer releaseRepo:'maven-releases', snapshotRepo:'maven-snapshots', server: server
//   // rtMaven.resolver releaseRepo:'maven-releases', snapshotRepo:'maven-snapshots', server: server

//   rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
//   rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server

//   rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo

//   buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
//   // Publish build info.
//   server.publishBuildInfo buildInfo
// }


// Artifactory Upload Stage

        // stage("publish to nexus") 
        // {
        //           // Read POM xml file using 'readMavenPom' step , this step 'readMavenPom' is included in: https://plugins.jenkins.io/pipeline-utility-steps
        //             pom = readMavenPom file: "pom.xml";
        //             // Find built artifact under target folder
        //             filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
        //             // Print some info from the artifact found
        //             echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
        //             // Extract the path from the File found
        //             artifactPath = filesByGlob[0].path;
        //             // Assign to a boolean response verifying If the artifact name exists
        //             artifactExists = fileExists artifactPath;
        //             if(artifactExists) {
        //                 echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
        //                 nexusArtifactUploader(
        //                     nexusVersion: NEXUS_VERSION,
        //                     protocol: NEXUS_PROTOCOL,
        //                     nexusUrl: NEXUS_URL,
        //                     groupId: pom.groupId,
        //                     version: pom.version,
        //                     repository: NEXUS_REPOSITORY,
        //                     credentialsId: NEXUS_CREDENTIAL_ID,
        //                     artifacts: [
        //                         // Artifact generated such as .jar, .ear and .war files.
        //                         [artifactId: pom.artifactId,
        //                         classifier: '',
        //                         file: artifactPath,
        //                         type: pom.packaging],
        //                         // Lets upload the pom.xml file for additional information for Transitive dependencies
        //                         [artifactId: pom.artifactId,
        //                         classifier: '',
        //                         file: "pom.xml",
        //                         type: "pom"]
        //                     ]
        //                 );
        //             } else {
        //                 error "*** File: ${artifactPath}, could not be found";
        //             }
        //         }
// End of Artifactory upload Stage

}