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
                deploy adapters: [tomcat9(credentialsId: '9fcc54b9-3f06-46e0-81e4-514750b2f7da', path: '', url: 'http://172.31.85.244:8080')], contextPath: 'app1', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '9fcc54b9-3f06-46e0-81e4-514750b2f7da', path: '', url: 'http://172.31.80.186:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    }
}
