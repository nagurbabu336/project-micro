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
       sh "cd /home/ubuntu/workspace/pipeline-java/discovery-service ; mvn clean install ;
        nexusArtifactUploader artifacts: [[artifactId: 'sample-spring-microservices', classifier: '', file: '/target/*.jar', type: 'jar']], credentialsId: 'nexus-pwd', groupId: 'pl.piomin', nexusUrl: '54.166.176.163:8081/nexus', nexusVersion: 'nexus3', protocol: 'http', repository: 'devop-mvn', version: 'gateway-service-1.0-SNAPSHOT'" 
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
