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
       sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; mvn clean install ; mvn test " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; sudo docker tag customer-service nagurbabu/account-service "
        sh "cd /home/ubuntu/workspace/accountservice-pipline/account-service ; sudo docker push nagurbabu/account-service  "
        
        
    }
}
 
   
stage ('k8sdeployment') 
    {
       steps {
           node (' ansible') {
             sh " sudo ansible-playbook /root/account-service.yml "
   
    }
}
}
}
    
    
}
