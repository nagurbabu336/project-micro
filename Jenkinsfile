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
  stage("sonar quality check"){
            steps {
             sh "cd /var/lib/jenkins/workspace/accountservice/account-service;  
                mvn sonar:sonar \
                -Dsonar.projectKey=account-service \
                -Dsonar.host.url=http://54.163.202.8:9000 \
                -Dsonar.login=ecf2fb2099b97799503afffaf96ef5c320398515; "
            
         }
              }
stage ('Build') 
{
    steps
    {
       sh "cd /var/lib/jenkins/workspace/accountservice/account-service; mvn clean install ; " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /var/lib/jenkins/workspace/accountservice/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd  /var/lib/jenkins/workspace/accountservice/account-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /var/lib/jenkins/workspace/accountservice/account-service ; sudo docker tag account-service nagurbabu/account-service "
        sh "cd /var/lib/jenkins/workspace/accountservice/account-service; sudo docker push nagurbabu/account-service  "
        
        
    }
}
}   
}
