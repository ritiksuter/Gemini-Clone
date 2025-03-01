pipeline{
    agent { label "ritik" }
    stages{
        stage("Code"){
            steps{
                echo "Here the developer have to code"
                git url: "https://github.com/ritiksuter/Gemini-Clone.git", branch:"main"
            }
        }
        stage("Build"){
            steps{
                echo "Here we are building the project"
                sh "docker build -t ritiksuteri/gemini-clone-app:v2 ."
                echo "Code builded successfully"
            }
        }
        stage("Push"){
            steps{
                echo "Here we need to Push the image to dockerHub"
                withCredentials([usernamePassword(credentialsId: 'secretCred', passwordVariable: 'dockerHubPass', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ritiksuteri/gemini-clone-app:v2"
                }
                echo "Docker image pushed successfully"
            }
        }
        stage("Deploy"){
            steps{
                echo "Here we need to deploy the code"
                sh "docker run -p 5173:5173 -d ritiksuteri/gemini-clone-app:v2"
            }
        }
    }
}







// @Library('Shared') _
// pipeline{
//     agent { label 'ritik'}
    
//     stages{
//         stage("Code"){
//             steps{
//                 code()
//             }
//         }
//         stage("Build"){
//             steps{
//                 build()
//             }
//         }
//         stage("Push"){
//             steps{
//                 push()
//             }
//         }
//         stage("Deploy"){
//             steps{
//                 deploy()
//             }
//         }
//     }
// }
