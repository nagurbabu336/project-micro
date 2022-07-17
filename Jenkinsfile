pipeline {
agent any 
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
       sh "cd /home/ubuntu/workspace/customerservice-pipeline/customer-service ; mvn clean install " 
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; mvn clean install " 
        sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service ; mvn clean install " 
        sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/customerservice-pipeline/customer-service; sudo docker build -t customer-service . " 
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service; sudo docker build -t customer-service . " 
        sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service; sudo docker build -t customer-service . " 
        sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service; sudo docker build -t customer-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/customerservice-pipeline/customer-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/customerservice-pipeline/customer-service ; sudo docker tag customer-service nagurbabu/customer-service "
        sh "cd /home/ubuntu/workspace/customerservice-pipeline/customer-service ; sudo docker push nagurbabu/customer-service  "
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; sudo docker tag account-service nagurbabu/account-service "
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; sudo docker push nagurbabu/account-service  "
        sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service ; sudo docker tag discovery-service nagurbabu/discovery-service "
        sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service ; sudo docker push nagurbabu/discovery-service  "
               sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; sudo docker tag gateway-service nagurbabu/gateway-service "
        sh "cd /home/ubuntu/workspace/gatewayservice-pipeline/gateway-service ; sudo docker push nagurbabu/gateway-service  "
        
        
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
