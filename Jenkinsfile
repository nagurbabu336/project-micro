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
       sh "cd /home/ubuntu/workspace/pipeline-java/customer-service ; mvn clean install " 
    }
}
   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/pipeline-java/customer-service; sudo docker build -t customer-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/pipeline-java/customer-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/pipeline-java/customer-service ; sudo docker tag customer-service nagurbabu/customer-service "
        sh "cd /home/ubuntu/workspace/pipeline-java/customer-service ; sudo docker push nagurbabu/customer-service  "
        
        
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
