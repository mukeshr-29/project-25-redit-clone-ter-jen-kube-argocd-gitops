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
                    sed -i 's|\\(image: mukeshr29/reddit-clone\\):.*|\\1:${IMAGE_TAG}|' deployment.yml
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
