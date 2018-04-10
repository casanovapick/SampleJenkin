
def GIT_URL = 'https://github.com/CyberioMor/uchoose_android.git'
node {
   stage('Preparation') {
      git url: "${GIT_URL}" ,branch: "${BRANCH.replaceAll(".*/","")}"
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
      archiveArtifacts '**/*.apk'
      nexusArtifactUploader credentialsId: '9e07136b-6e35-30d7-9ba3-6875aba28529', groupId: 'uchoose', nexusUrl: 'localhost:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'maven-snapshots', version: '1.0.0'
   }
}