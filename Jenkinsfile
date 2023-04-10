pipeline{
    agent {
  label 'docker'
} 
environment {
		DOCKER_LOGIN_CREDENTIALS=credentials('dockerhostpush')
	}
    stages {
  stage('checkout') {
    steps {
      git 'https://github.com/DivyaChilukuri/hello-world-war.git'
    }
  }

  stage('build') {
    steps {
      sh 'mvn clean install'
      sh 'docker build -t divyachilukuri/divya:$BUILD_NUMBER .' 

    }
  }

  stage('push') {
    steps {
      sh 'echo $DOCKER_LOGIN_CREDENTIALS_PSW | docker login -u $DOCKER_LOGIN_CREDENTIALS_USR --password-stdin'
      sh 'docker push divyachilukuri/divya:$BUILD_NUMBER'
    }
  }

  stage('deploy') {
    steps {
      sh "docker run -itd -p 8080:8080 divyachilukuri/divya:$BUILD_NUMBER"
    }
  }

}

}
