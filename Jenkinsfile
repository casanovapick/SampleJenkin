
def GIT_URL = 'https://github.com/CyberioMor/uchoose_android.git'
node {

   stage('Preparation') {
      git GIT_URL
   }

   stage('Stage Build') {
      sh "./gradlew clean"
   }

   stage('Stage Unit Tests') {
      sh "./gradlew testReleaseUnitTest"
   }

   stage('Pack') {
      sh "./gradlew clean assembleDevelopDebug"
      sh "./gradlew clean assembleProductionRelease"
   }
}