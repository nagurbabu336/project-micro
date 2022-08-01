pipeline {
agent 'any'

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
       sh "cd /var/lib/jenkins/workspace/account-service/account-service; mvn clean install ; " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /var/lib/jenkins/workspace/account-service/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd  /var/lib/jenkins/workspace/account-service/account-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /var/lib/jenkins/workspace/account-service/account-service ; sudo docker tag account-service nagurbabu/account-service "
        sh "cd /var/lib/jenkins/workspace/account-service/account-service; sudo docker push nagurbabu/account-service  "
        
        
    }
}
 
      stage ('K8S Deploy') {
       
                kubernetesDeploy(
                    configs: 'MyAwesomeApp/springboot-lb.yaml',
                    kubeconfigId: 'k8s',
                    enableConfigSubstitution: true
                    )               
        }
    
}   

}
    
    
}
