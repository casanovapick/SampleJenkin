
def GIT_URL = 'https://github.com/CyberioMor/uchoose_android.git'
node {
   stage('Preparation') {
      git url: "${GIT_URL}" ,branch: "${BRANCH.replaceAll(".*/","")}"
      sh "git clean -fdx"
      sh "./gradlew clean"
   }

   stage('Unit Tests') {
      sh "./gradlew testDevelopDebug"
   }

   stage('Static code analysis'){
      def workspace = pwd() 
      def SONAR_SETTING = "${workspace}@script/sonar-project.properties"
      sh "/Users/wannnasit.chaiphinan/Library/SonarScanner/bin/sonar-scanner  -Dproject.settings=${SONAR_SETTING}"
   }

   stage('Packaging') {
      sh "./gradlew assembleDevelopDebug --offline"
      sh "./gradlew assembleProductionRelease --offline"
   }

   stage('Upload'){
      sh "zip -r artifact.zip . -i *.apk"
      nexusArtifactUploader artifacts: [[artifactId: 'uchoose', classifier: '', file: 'artifact.zip', type: 'zip']], credentialsId: 'cedf432b-2dd2-4e3c-ae6a-11780cf6244d', groupId: 'mobile.android', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '1.0.0'
   }
}