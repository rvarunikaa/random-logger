#!groovy
node('dockerinside') 
{
    stage('Checkout') {
        checkout scm;
    }
    stage('Docker image creation') {
        currentStep = "CREATE IMAGE "
        echo "Building docker image"

        withCredentials(
            [usernamePassword(
                            credentialsId: "ARTIFACTORY_BAGGAGE",
                            passwordVariable: 'password',
                            usernameVariable: 'user')])
        {
            echo "Docker Image creation"
            def sourceTag = "artifacts.aa.com/docker-all/baggage/infra/sample-ltu-logger:0.0.1"
            def app = docker.build(sourceTag, "-f ./Dockerfile .")
            echo "Docker push - ImageName: " + sourceTag
            app.push("0.0.1")
        }
        echo 'Dockerizing the build :: END'
    }
}
