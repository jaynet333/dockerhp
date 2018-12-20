node {
    def app
    stage('Build Docker Image') {
        checkout scm
        app = docker.build('jstage/sample-app:latest')
    }
    
    stage('Publish to Docker Hub') {
        docker.withRegistry("https://hub.docker.com/", "dockerhub") {
            app.push('latest')
        }
    }

    stage('Deploy to Production') {
        docker.withServer('tcp://symapltest01vm2:2376', 'production') {
            sh 'docker run -d dockerhp/sample-app'
        }
    }
}
