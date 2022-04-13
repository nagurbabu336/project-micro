pipeline {
agent {
label 'buildserver'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('upload') 
{
    steps
    {
       nexusArtifactUploader credentialsId: 'nexus-login', groupId: '', nexusUrl: '54.159.194.44:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://54.159.194.44:8081/repository/maven-jar-backup/', version: ''
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service; sudo docker build -t  gateway-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; sudo docker tag  gateway-service nagurbabu/gateway-service "
        sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; sudo docker push nagurbabu/gateway-service "
        
        
    }
}
 
   
stage ('k8sdeployment') 
    {
       steps {
           node (' ansible') {
             sh " sudo ansible-playbook /root/k8s.yml"
   
    }
}
}
}
    
    
}
