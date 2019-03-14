//*properties([pipelineTriggers([pollSCM('')])])

node{

   //pipeline varibale definition
   def tomcatIp = '172.31.20.233'
   def tomcatUser = 'ec2-user'
   
   //echo env.BUILD_NUMBER
   //def BUILD_ID = env.BUILD_NUMBER
    
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
//    
    stage('Anisble Playbook- publish warfile in Host machine'){
    
    sh label: '', script: 'cp /var/lib/jenkins/workspace/Pipeline_All/target/petclinic.war /opt/ansible/warfiles'
  
    sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible-server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /opt/ansible/playbooks/copywarfile.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
  }
        
}
