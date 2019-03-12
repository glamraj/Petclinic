properties([pipelineTriggers([pollSCM('')])])

node{
    
   //pipeline varibale definition
   def tomcatIp = '172.31.20.233'
   def tomcatUser = 'ec2-user'
    
    stage('Introduction'){
        
    echo 'Hello-- Welcome to Pipeline Demo'
  }
    
    stage('SCM Checkout'){
        
    git 'https://github.com/glamraj/Petclinic.git'
  }

    stage('Maven Build'){ 
    
    //get Maven home path
    def mvnHome = tool name: 'M2', type: 'maven'
    sh "${mvnHome}/bin/mvn clean package"
  }
    
    stage('Build Docker Imager'){
  
    sh 'docker build -t dockerglam/petclinic:1.0 .'
 }
    
}
