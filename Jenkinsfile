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
 		    docker.withRegistry('https://registry.hub.docker.com', 'dockerhubruno') {
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

       stage('Teste Aplicação') {
 	  steps {
 	      // Testes automatizados da aplicação
 	      sh 'docker-compose -f docker-compose.yml up -d'
 	
	      // Realize os testes nos serviços em execução
 	      // Exemplo de teste usando curl para verificar se o serviço web está respondendo
 	      sh 'curl -I http://localhost'
 	
	      sh 'docker-compose -f docker-compose.yml down'
 	  }	
       }
       stage('Aprovação') {
       	   steps {
	       input 'Deseja prosseguir com o Deploy e Push?'	
           }
       }		
   }
}

