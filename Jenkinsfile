node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    if (env.BRANCH_NAME == 'dev') {
    stage('Build image') {
       app = docker.build("borismanev/jenkins-tes")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'docekrhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
    }
}
