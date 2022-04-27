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
       sh "cd /home/ubuntu/workspace/pipeline-java/discovery-service ; mvn clean install ; " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/pipeline-java/discovery-service; sudo docker build -t discovery-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service ; sudo docker tag discovery-service nagurbabu/discovery-service "
        sh "cd /home/ubuntu/workspace/discoveryservice-pipeline/discovery-service ; sudo docker push nagurbabu/discovery-service  "
        
        
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
