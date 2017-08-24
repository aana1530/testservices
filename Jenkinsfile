#!/usr/bin/env groovy
node {
   def mvnHome
   def version
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      //git 'https://github.com/aana1530/addressbook.git'
       //def text = new FileInputStream("/root/.jenkins/workspace/A1/ip.properties").getText().readLines().get(2)
        String fileContents = new File('/root/.jenkins/id.properties').text.readLines().get(1)
      println fileContents
	   def libName = params.list
	   println list
	 //  println ${list}
        //a = text.toString()
    //    println a
        //sh '"echo $a" > /tmp/file'
       // cr = readFile '/tmp/file'
      //  def ret = sh(script: "'echo $a'", returnStdout: true)
//println ret
        //sh var = $("echo $a")'
       // var = 'sh "echo $a"'
      //  println var
        //println text
       // git text
    //   git "$fileContents"
   //  git([url: "${fileContents}", branch: "$list"])
 //  git([url: "git@gitlab.dxide.com:sapient/alcs-devops-cm.git", branch: "$list"])
	   git([url: "https://"sapient-builder":\"'YXP2@Fg&n3WpDS+7'\"@gitlab.dxide.com/sapient/alcs-aem-backend.git", branch: "$list"])
//	 sh "git clone '${fileContents}'"
// sh " cd alcs-aem-backend ;git checkout '$list'"
      
    //  sh "cp -r alcs-aem-backend/* ."
	 
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven'
      version='3.3.9'
      //echo "\u2600 BUILD_URL=${env.JENKINS_URL}"
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean install "
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean install/)
      }
   }
  // stage('Results') {
    //  junit '**/target/surefire-reports/TEST-*.xml'
      //archive 'target/*.jar'
  // }
   stage('Sonar Analysis') {
      build 'Sonar'
      withSonarQubeEnv('Sonar') {
      sh 'mvn clean install sonar:sonar'
      }
   }
  
//  stage('SonarQube analysis') {
  //  withSonarQubeEnv('SONAR') {
      // requires SonarQube Scanner for Maven 3.2+
    //  sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
//    }
 // }
  // stage('Publish') {
    // nexusPublisher nexusInstanceId: 'NEXUS', nexusRepositoryId: 'Release', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'addressbook_main/target/addressbook.war']], mavenCoordinate: [artifactId: 'addressbook_main', groupId: 'com.edurekademo.tutorial', packaging: 'war', version: '2.3.0']]]
   //}
   //stage('Deploy approval'){
    //input "Deploy to prod?"
//}

  //  stage('Send E-mail'){
    //    emailext body: 'Deployment Approved by MANAGER', subject: 'Deployment Approved', to: 'aashna1516@yahoo.com'
    //}
   
   stage('Deploy To AEM'){
       String fileip = new File('/root/.jenkins/id.properties').text.readLines().get(0)
      println fileip
      env.b = fileip
      println env.b
      //a = fileip.toSring
     // println a
//     def command = sh "echo ${fileip}"
  //   println command
   //  fileip1 = sh(returnStdout: true, script: command).trim()
//    sh("echo ${fileip1}")
    sh """curl -u admin:admin -F file=@"$WORKSPACE/ui/target/alcs-backend-1.0-SNAPSHOT.zip" -F name="alcs-backend-1.0-SNAPSHOT.zip" -F force=true -F install=true http://'''${env.b}''':4502/crx/packmgr/service.jsp
"""

    }
}

