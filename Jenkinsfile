
def GIT_URL = 'https://github.com/CyberioMor/uchoose_android.git'
node {
   stage('Preparation') {
      git url: "${GIT_URL}" ,branch: "${BRANCH.replaceAll(".*/","")}"
   }

   stage('Stage Build') {
      sh "./gradlew clean"
   }

   stage('Stage Unit Tests') {
      sh "./gradlew test"
   }

   stage('Static code analysis'){
      def workspace = pwd() 
      def SONAR_SETTING = "${workspace}@script/sonar-project.properties"
      sh "/Users/wannnasit.chaiphinan/Library/SonarScanner/bin/sonar-scanner  -Dproject.settings=${SONAR_SETTING}"
   }

   stage('Pack') {
      sh "./gradlew clean assembleDevelopDebug"
      sh "./gradlew clean assembleProductionRelease"
   }
}