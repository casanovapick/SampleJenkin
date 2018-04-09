
def GIT_URL = 'https://github.com/CyberioMor/uchoose_android.git'
node {
   def ANDROID_HOME='/Users/wannnasit.chaiphinan/Library/Android/sdk'
   stage('Preparation') {
      git GIT_URL
   }

   stage('Stage Build') {
      sh "./gradlew clean"
   }

   stage('Stage Unit Tests') {
      sh "./gradlew testReleaseUnitTest"
   }

   stage('Static code analysis'){
      def SONAR_SETTING = scriptPath("sonar-project.properties")
      sonar-scanner SONAR_SETTING
   }

   stage('Pack') {
      sh "./gradlew clean assembleDevelopDebug"
      sh "./gradlew clean assembleProductionRelease"
   }
}