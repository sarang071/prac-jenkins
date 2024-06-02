pipeline{
    agent any


    stages{

        stage('Test'){
            steps {
            echo "first script"
            checkout scm
            echo -e "$GIT_COMMIT"
            }

        }
    }
}