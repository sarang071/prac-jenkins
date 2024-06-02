pipeline{
    agent any
    environment{
        registryURI = "https://registry.hub.docker.com/"
        registry = "sarangp007/sample-nginx-qa"
        registryCreds = '01'
    }

    stages{

        // stage('Checkout SCM'){

        //     steps{
        //         git ''
        //     }
        // }

        stage('build'){
            steps{
                script{
                    def docker_app = docker.build("$env.registryURI" + ":" + "$GIT_COMMIT")
                }
            }
        }
        stage('Deploy Image'){
            environment{
                registry_endpoint = "$env.registryURI" + "$env.registry"
            }
            steps{
                script{
                    docker.withRegistry("$env.registry_endpoint",registryCreds){
                        docker_app.push()
                        docker_app.push(latest)
                    }
                }
            }
        }


    }

}