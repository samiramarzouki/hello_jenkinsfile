pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        image_tag='docker.pkg.github.com/samira1/hello_jenkinsfile/cockpitapp:${GIT_COMMIT}'
        cred=credentials('github-new')
        
    }
    
    stages{
        
       
        stage("Building docker image")
        {
            steps{
                sh "docker build -t $image_tag ."
            }
        }
        stage("push image to github repo")
        {
            steps{
                sh """ 
                echo $cred_PSW | docker login docker.pkg.github.com -u $cred_USR --password-stdin 
                docker push $image_tag
                """
            } 
        }
    }
}
