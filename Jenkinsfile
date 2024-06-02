pipeline{
    agent any
    environment {
        RegistryURL = " https://registry.hub.docker.com"
        RepoName = "sarangp007/sample-nginx-qa"
        dh_creds = "dockerhub_creds"
    }

    stages{
        stage('build image') {
            environment {
                registry_endpoint = "${env.RegistryURL}" + "${env.RepoName}"
                tag = "${env.RepoName}" + ":$GIT_COMMIT"
                file_path = "${workspace}/"
            }
            steps{
                script{
                    dockerwithRegistry(registry_endpoint,dh_creds)
                    def Img = docker.build(tag,file_path)

                    Img.push()
                }
            }
        }
    }
}