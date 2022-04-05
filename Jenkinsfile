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
       sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; mvn sonar:sonar \
  -Dsonar.projectKey=gateway-service \
  -Dsonar.host.url=http://18.233.164.34:9000 \
  -Dsonar.login=290871a21cb18cc4b7671456b031b2a0cf8455b5 " 
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
