node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("van40s/jenkins_repo")
    }
    stage('Push image') {
        withDockerRegistry([credentialsId: 'dockerhub', url: 'https://registry.hub.docker.com']) {
            sh "docker push ${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
            sh "docker push ${env.BRANCH_NAME}-latest"
            // signal the orchestrator that there is a new version
        }
    }
}
