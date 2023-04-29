pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                    
             git 'https://github.com/intelliqittrainings/maven.git'   
            }
        }
      stage('ContBuild')
      {
          steps
          {
             sh 'mvn package' 
          }
      }
      stage('ContDeployment')
      {
          steps
          {
            deploy adapters: [tomcat9(credentialsId: 'f2f00a6e-0e49-4929-a83d-79094989181f', path: '', url: 'http://172.31.94.0:8080')], contextPath: 'test1', war: '**/*.war'  
          }
      }
      stage('ContTesting')
      {
          steps
          {
            git 'https://github.com/intelliqittrainings/FunctionalTesting.git' 
            sh '''java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'''
          }
      }
      stage('ContDelivery')
      {
          steps
          {
            deploy adapters: [tomcat9(credentialsId: 'f2f00a6e-0e49-4929-a83d-79094989181f', path: '', url: 'http://172.31.87.75:8080')], contextPath: 'prod1', war: '**/*.war'  
          }
      }
    }
}
