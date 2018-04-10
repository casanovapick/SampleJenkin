
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
      nexusArtifactUploader artifacts: [[artifactId: 'android', classifier: '', file: '**/*.apk', type: 'apk']], credentialsId: '', groupId: 'uchoose', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0.0'
   }
}