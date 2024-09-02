node {
    def dockerRegistry = 'https://registry.hub.docker.com'
    def dockerCredentialsId = 'dockerhub-credentials-id'
    def imageName = 'fansari9993/test9'
    def imageTag = 'tagname'
    def image

    try {
        stage('Source Code Checkout') {
            checkout([
                $class: 'GitSCM',
                branches: [[name: '*/main']],
                doGenerateSubmoduleConfigurations: false,
                extensions: [],
                userRemoteConfigs: [[url: 'https://github.com/faraz9993/dock_jen.git']]
            ])
        }

        stage('Build Docker Image') {
            image = docker.build("${imageName}:${imageTag}")
        }

        stage('Push Docker Image') {
            docker.withRegistry("${dockerRegistry}", "${dockerCredentialsId}") {
                image.push()
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        echo "Pipeline failed: ${e.message}"
    } finally {
        echo "Cleaning up workspace..."
        cleanWs()
    }
}
