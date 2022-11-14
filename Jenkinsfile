pipeline{
    agent any
    
    stages{
        stage('Clone the springboot-cicd deployment repo'){
            steps{
                git branch: 'main', credentialsId: 'git-credentials', url: 'https://github.com/parthaSdeb/springboot-cicd-deployment.git'
            }
        }
        
        stage('Update the deployment file'){
            steps{
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    
                    withCredentials([gitUsernamePassword(credentialsId: 'git-credentials', gitToolName: 'Default')]) {
                        
                        echo "build no is : $DockerTag"
                        
                        sh "git config user.email parthadeb95@gmail.com"
                        
                        sh "git config user.name parthaSdeb"
                        
                        sh "cat springboot-cicd.yaml"
                        
                        
                        sh "sed -i 's+registry.tirzok.com:5000/springboot-cicd-dynamic.*+registry.tirzok.com:5000/springboot-cicd-dynamic:${DockerTag}+g' springboot-cicd.yaml"
                        
                        sh "cat springboot-cicd.yaml"
                        
                        sh "git add ."
                        
                        sh "git commit -m 'Done by Jenkins Job update-deployment: ${env.BUILD_NUMBER}'"
                        
                        sh "git push origin main"

                    }
                }
            }
            
        }
    }
}
