pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_loans') 
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
                        mail bcc: '', body: 'Jenkins is unable to download the code from github', cc: '', from: '', replyTo: '', subject: 'Download failed', to: 'git.team@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild_loans') 
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to build artifact from code', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'development.team@gmail.com'
                        exit(1)
                    }
                }
            }
        }
     }
}
