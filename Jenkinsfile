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
stage ('Build') 
{
    steps
    {
        withSonarQubeEnv(credentialsId: 'sonar-token')
       sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; mvn sonar:sonar 
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
