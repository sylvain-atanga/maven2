pipeline
{
    agent any
    stages
    {
        stage('continous download')
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
                        mail bcc: '', body: 'download has failed for unknown reason', cc: '', from: '', replyTo: '', subject: 'download fail', to: 'SCMmanagementteam@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('continous build')
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
                        mail bcc: '', body: 'build has failed for unknown reason', cc: '', from: '', replyTo: '', subject: 'build fail', to: 'developersteam@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('continous deployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '3b4e088a-e578-4718-864c-9402c96c07bf', path: '', url: 'http://10.0.13.6:8080')], contextPath: 'errorapp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'deployment has failed for unknown reason', cc: '', from: '', replyTo: '', subject: 'deployment fail', to: 'middlewareteam@gmail.com'
                        exit(1)                    }
                }
                
            }
        }
        stage('continous testing')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/sylvain-atanga/FunctionalTesting.git'
                        sh 'java -jar /var/lib/jenkins/workspace/PIPELINES/CICD/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'testing has failed for unknown reason', cc: '', from: '', replyTo: '', subject: 'testing fail', to: 'testingteam@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('continous delivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        input message: 'Waiting for interactive from DM', submitter: 'Ijombe'
                        deploy adapters: [tomcat9(credentialsId: '6bc6efc7-ce58-4ba0-a4fb-35584d4c2023', path: '', url: 'http://10.0.11.157:8080')], contextPath: 'errorprodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'delivery has failed for unknown reason', cc: '', from: '', replyTo: '', subject: 'delivery fail', to: 'deliveryteam@gmail.com'
                        exit(1)
                    }
                }
            }
        }
    }
}
