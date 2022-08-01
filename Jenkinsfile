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
       sh "cd /var/lib/jenkins/workspace/account-service/account-service ; mvn clean install " 
    }
}
    stages{
        stage("sonar quality check"){
            agent {
                docker {
                    image 'openjdk:11'
                }
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar') {
                            sh 'mvn sonar'
                    }

                    timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }

                }  
            }
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
       sh "cd var/lib/jenkins/workspace/account-service/account-service ; sudo  docker login $docker "
        sh "cd var/lib/jenkins/workspace/account-service/account-service ; sudo docker tag customer-service nagurbabu/account-service "
        sh "cd var/lib/jenkins/workspace/account-service/account-service ; sudo docker push nagurbabu/account-service  "
        
        
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
