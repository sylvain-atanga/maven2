pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_master')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/sylvain-atanga/Maven.git'
                    }
                    catch(Exception e1) 
                    {
                        mail bcc: '', body: 'jenkins has failed to download code from github', cc: '', from: '', replyTo: '', subject: 'Download has failed', to: 'gitadmin@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild_master')
        {
            steps
            {
                script
                {
                     try
                    {
                        sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'jenkins has failed to build the code', cc: '', from: '', replyTo: '', subject: 'build has failed', to: 'devteam@gmail.com'
                        exit(1)
                    }    
                }
                
            }
        }
        stage('ContinuousDeployment_master')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '5e216110-9656-45c8-bc75-bec87ddd167d', path: '', url: 'http://172.31.95.216:8080')], contextPath: 'testappp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'jenkins has failed to deploy artifact to tomcat server', cc: '', from: '', replyTo: '', subject: 'deployment has failed', to: 'middlewareteam@gmail.com'
                        exit(1)
                    }
                }
                
            }
        }
        stage('ContinuousTesting_master')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/sylvain-atanga/FunctionalTesting.git'
                        sh 'java -jar /var/lib/jenkins/workspace/ExceptionsDeclarative/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'selenium scripts have failed to test artifact', cc: '', from: '', replyTo: '', subject: 'testing has failed', to: 'testingteam@gmail.com'
                        exit(1)
                    }
                }
                
                
            }
        }
        stage('ContinuousDelivery_master')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '5e216110-9656-45c8-bc75-bec87ddd167d', path: '', url: 'http://172.31.90.31:8080')], contextPath: 'prodappp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'jenkins has failed to deliver artifact to tomcat prodserver', cc: '', from: '', replyTo: '', subject: 'delivery has failed', to: 'Deliveryteam@gmail.com'
                    }
                    
                    
                    
                }
                
            }
            
        }
    }
}
  
