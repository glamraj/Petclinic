properties([pipelineTriggers([pollSCM('')])])

node{
    
    stage('Introduction'){
    echo 'Hello-- Welcome to Pipeline Demo'
  }
    
    stage('SCM Checkout'){
    git 'https://github.com/glamraj/Petclinic.git'
  }

    stage('Maven Build'){ 
    tool name: 'M3', type: 'maven'
    sh label: '', script: 'mvn clean package'
  }
       
}
