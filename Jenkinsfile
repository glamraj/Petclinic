properties([pipelineTriggers([pollSCM('')])])

node{
    
   def tomcatIp = '172.31.17.253'
   def tomcatUser = 'ec2-user'
   def stopTomcat = "ssh ${tomcatUser}@${tomcatIp} /opt/apache-tomcat-8.5.38/bin/shutdown.sh"
   def startTomcat = "ssh ${tomcatUser}@${tomcatIp} /opt/apache-tomcat-8.5.38/bin/startup.sh"
   def copyWar = "scp -o StrictHostKeyChecking=no target/petclinic.war ${tomcatUser}@${tomcatIp}:/opt/apache-tomcat-8.5.38/webapps/"
    
    stage('Introduction'){
    echo 'Hello-- Welcome to Pipeline Demo'
  }
    
    stage('SCM Checkout'){
    git 'https://github.com/glamraj/Petclinic.git'
  }

    stage('Maven Build'){ 
    tool name: 'M2', type: 'maven'
    sh label: '', script: 'mvn clean package'
  }
    
    stage('JUnit Publisher'){ 
    junit allowEmptyResults: true, testResults: '/var/lib/jenkins/workspace/Petclinic/target/surefire-reports/**.xml'
  }
    
    stage('Deploy to Tomcat'){
    sh label: '', script: 'mv target/*.war target/petclinic.war'
        
    sshagent(['linux-host']) {
    sh "${stopTomcat}"
        
    sh 'ssh ec2-user@172.31.17.253 rm -rf /opt/apache-tomcat-8.5.38/webapps/petclinic*'
    sh "${copyWar}"
	sh "${startTomcat}"
    }
  }
    
}
