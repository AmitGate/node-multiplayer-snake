node ('ubuntu') {
    def app

    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm
    }

    stage('Build-and-Tag') {
        /* This builds the actual image; synonymous to docker build on the command line */
        app = docker.build("amitgate/snake")
    }

    stage('Post-to-dockerhub') {
        /* Authenticate to Docker Hub and push the image */
        withDockerRegistry([credentialsId: 'amitdock_creds', url: 'https://index.docker.io/v1/']) {
            // Push the image to Docker Hub
            app.push("latest")
        }
    }

    stage('Pull-image-server') {
        /* Pull the image on the server and start it using Docker Compose */
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}

