@Library("Shared_Lib") _
pipeline
{
    
    agent { label "alex" }
    
    stages
    {
        stage("Git clone")
        {
            steps
            {
                script
                {
                    clone("https://github.com/vaibhavbharambe2/Jenkins-Project-TwoTierDeployment.git","main")
                }
            }
        }
        stage("Docker build")
        {
            steps
            {
                script
                {
                    build("two-tier-deployment","latest","vaibhav237")
                }
            }
        }
        stage("Dcoker run")
        {
            steps
            {
                script
                {
                    deploy()
                }
            }
        }
        stage("Docker push")
        {
            steps
            {
                script
                {
                    PushImage("two-tier-deployment","latest","vaibhav237")
                }
            }
        }
    }
    post {
        success {
            script {
                emailext attachLog: true,
                from: 'vaibhavbharambe2@gmail.com',
                subject: "Two-Tier application has been updated and deployed - '${currentBuild.result}'",
                body: """
                    <html>
                    <body>
                        <div style="background-color: #FFA07A; padding: 10px; margin-bottom: 10px;">
                            <p style="color: black; font-weight: bold;">Project: ${env.JOB_NAME}</p>
                        </div>
                        <div style="background-color: #90EE90; padding: 10px; margin-bottom: 10px;">
                            <p style="color: black; font-weight: bold;">Build Number: ${env.BUILD_NUMBER}</p>
                        </div>
                        <div style="background-color: #87CEEB; padding: 10px; margin-bottom: 10px;">
                            <p style="color: black; font-weight: bold;">URL: ${env.BUILD_URL}</p>
                        </div>
                    </body>
                    </html>
            """,
            to: 'vaibhavbharambe2@gmail.com',
            mimeType: 'text/html'
            }
        }
      failure {
            script {
                emailext attachLog: true,
                from: 'vaibhavbharambe2@gmail.com',
                subject: "Two-Tier application build failed - '${currentBuild.result}'",
                body: """
                    <html>
                    <body>
                        <div style="background-color: #FFA07A; padding: 10px; margin-bottom: 10px;">
                            <p style="color: black; font-weight: bold;">Project: ${env.JOB_NAME}</p>
                        </div>
                        <div style="background-color: #90EE90; padding: 10px; margin-bottom: 10px;">
                            <p style="color: black; font-weight: bold;">Build Number: ${env.BUILD_NUMBER}</p>
                        </div>
                    </body>
                    </html>
            """,
            to: 'vaibhavbharambe2@gmail.com',
            mimeType: 'text/html'
            }
        }
    }
    
}
