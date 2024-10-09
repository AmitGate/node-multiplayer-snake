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
    
     withDockerRegistry([credentialsId: 'amitdock_creds', url: 'https://index.docker.io/v1/']) {
    sh 'docker build -t amitgate/snake .'
	}
 	{
            app.push("latest")
        			}
         }
  
    
    stage('Pull-image-server') {
    
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }
 
}
