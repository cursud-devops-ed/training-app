node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/cursud-devops-ed/training-app'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven3'
   }
     
    stage('Test') {
      if (isUnix()) {
         
      } else {
         bat(/"${mvnHome}\bin\mvn" clean test/)
      }
   }  
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore  build"
      } else {
         bat(/"${mvnHome}\bin\mvn" -B -DskipTests -Dmaven.test.failure.ignore package/)
      }
   }
     
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts  'target/*.jar'
   }

      stage('Publish Artefact') {
       // 
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -DdeployOnly deploy"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.skip=true deploy -s "C:\apache-maven-3.6.0\conf\settings.xml"/)
      }//
   }
   
   stage('Execute Jar') {
      if (isUnix()) {
         sh "java -jar  target/*.jar"
      } else {
         bat(/java -jar target\/training-app-1.0-jar-with-dependencies.jar/)
      }
   }
}
