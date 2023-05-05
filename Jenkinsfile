pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
               git 'https://github.com/Anil3855/Jenkins-pipeline.git' 
            }
        }
        stage('ContBuild')
        {
          steps
          {
              sh 'mvn package'
          }
        }
        stage('contDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '24448151-b749-4df8-a64f-1cf7481d8030', path: '', url: 'http://172.31.10.192:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline1/testing.jar'
                
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                input message: 'Need approval from DM!', submitter: 'srinivas'
                deploy adapters: [tomcat9(credentialsId: '24448151-b749-4df8-a64f-1cf7481d8030', path: '', url: 'http://172.31.12.151:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
        
        
    }
}
