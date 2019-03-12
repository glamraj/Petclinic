properties([pipelineTriggers([pollSCM('')])])

node{
    
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
       
}
