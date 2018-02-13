echo 'Hello from Pipeline Demo' 
stage 'Compile' 
node { 
  git url: 'https://github.com/cemp2703/spring-petclinic.git' 
  def mvnHome = tool 'MAVEN_HOME' 
  sh "${mvnHome}/bin/mvn -B compile" 
} 
stage 'Test' 
node('WindowsNode') { 
  git url: 'https://github.com/cemp2703/spring-petclinic.git' 
  def mvnHome = tool 'MAVEN_HOME' 
  bat "${mvnHome}\\bin\\mvn -B verify" 
  step([$class: 'ArtifactArchiver', artifacts: '**/target/*.war', fingerprint: true])   
  step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml']) 
} 