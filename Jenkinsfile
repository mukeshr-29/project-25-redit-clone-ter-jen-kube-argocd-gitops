pipeline{
    agent any
    environment{
        APP_NAME = "reddit-clone"
    }
    stages{
        stage('clean work space'){
            steps{
                cleanWs()
            }
        }
        stage('git checkout'){
            steps{
                git credentialsId: 'github', url: 'https://github.com/mukeshr-29/project-25-redit-clone-ter-jen-kube-argocd-gitops.git'
            }
        }
        stage('update deployment file'){
            steps{
                sh """
                    cat deployment.yml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yml
                """
            }
        }
        stage('push changed deployfile to git hub'){
            steps{
                sh """
                    git config --global user.name "mukeshr-29"
                    git config --global user.email "mukeshr2911@gmail.com"
                    git add deployment.yml
                    git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]){
                    sh "git push https://github.com/mukeshr-29/project-25-redit-clone-ter-jen-kube-argocd-gitops.git master"
                }
            }
        }
    }
}