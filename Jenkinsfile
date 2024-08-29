pipeline {
    agent any
    environment {
 	DOCKERFILE_WEB = 'Dockerfileweb'
 	DOCKERFILE_DB = 'Dockerfiledb'
 	DOCKERFILE_NGINX = 'Dockerfilenginx'
 	DOCKER_IMAGE_TAG = 'latest'
    }
    stages {
 
	stage('Build Images') {
 	    steps {
 		script {
 		    // Nome das imagens
		    def imageNameWeb = 'bvieira020/web'
 		    def imageNameDB = 'bvieira020/db'
 		    def imageNameNginx = 'bvieira020/nginx'
 		    
		    // Executa o build das imagens com os respectivos Dockerfiles
 		    docker.withRegistry('https://registry.hub.docker.com', 'dockerhubvieira020') {
 			def webImage = docker.build("${imageNameWeb}:${DOCKER_IMAGE_TAG}", "-f ${DOCKERFILE_WEB} .")

		 	def dbImage = docker.build("${imageNameDB}:${DOCKER_IMAGE_TAG}", "-f ${DOCKERFILE_DB} .")
 
			def nginxImage = docker.build("${imageNameNginx}:${DOCKER_IMAGE_TAG}", "-f ${DOCKERFILE_NGINX} .")
 
			webImage.push()
 			dbImage.push()
 			nginxImage.push()
 		   }
 		}
 	   }
       }	
   }
}

