
def GIT_URL = 'https://github.com/CyberioMor/uchoose_android.git'
node {

   stage('Clean') {
      sh "./gradlew clean build"
   }

   stage('Preparation') {
      cleanWs()
      git url: "${GIT_URL}" ,branch: "${BRANCH.replaceAll(".*/","")}"
   }

   stage('Unit Tests') {
      sh "./gradlew test --offilne"
   }

   stage('Static code analysis'){
      def workspace = pwd() 
      def SONAR_SETTING = "${workspace}@script/sonar-project.properties"
      sh "/Users/wannnasit.chaiphinan/Library/SonarScanner/bin/sonar-scanner  -Dproject.settings=${SONAR_SETTING}"
   }

   stage('Packaging') {
      sh "./gradlew clean assembleDevelopDebug --offline"
      sh "./gradlew clean assembleProductionRelease --offline"
   }

   stage('Upload'){
      nexusArtifactUploader artifacts: [[artifactId: 'android', classifier: '', file: '**/*.apk', type: 'apk']], credentialsId: '', groupId: 'uchoose', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0.0'
   }
}