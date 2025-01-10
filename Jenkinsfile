

node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    // Configure Git user details with your GitHub account info
                    sh "git config user.email arunbaghel192004@gmail.com"
                    sh "git config user.name arunbaghel11"
                    
                    // Display deployment.yaml before and after modification
                    sh "cat deployment.yaml"
                    
                    // Replace the old Docker tag with the new one in deployment.yaml
                    sh "sed -i 's+arun662/react-app.*+arun662/react-app:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    
                    // Stage and commit changes
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    
                    // Push the changes securely
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                }
            }
        }
    }
}
