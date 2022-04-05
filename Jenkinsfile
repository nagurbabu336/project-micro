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
  -Dsonar.projectKey=gateway \
  -Dsonar.host.url= http://35.171.8.219:9000/
  -Dsonar.login=66088a46c5d5604057703ce2b46a455c1ebd57de "
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
