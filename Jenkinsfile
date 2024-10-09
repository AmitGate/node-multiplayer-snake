node ('ubuntu'){  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }  
    
    stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("amitgate/snake")
    }
    stage('Post-to-dockerhub') {
    
     docker.withRegistry('https://registry.hub.docker.com', 'amitdock_creds') {
            app.push("latest")
        			}
         }
  
    
    stage('Pull-image-server') {
    
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }
 
}

<<<<<<< HEAD

=======
>>>>>>> 8e41f5fb14d1b3edb6d4d267cf0f37cdf9009077
