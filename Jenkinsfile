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
    
    
    
}
