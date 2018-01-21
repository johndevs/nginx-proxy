pipeline {
  agent {
    label 'docker'
  }

  parameters {
     string(defaultValue: 'localhost:5000', description: 'Docker registry hostname and port', name: 'dockerRegistry')
     string(defaultValue: '1.0.${BUILD_NUMBER}', description: 'Build version', name: 'buildVersion')
  }

  stages { 
    stage('Build Image') {
      steps {
        sh "docker build \
	    -t com.devsoap/nginx-proxy:${params.buildVersion} \
	    -t ${params.dockerRegistry}/com.devsoap/nginx-proxy:${params.buildVersion} \
            ."
      }
    }

    stage('Deploy Image') {
      steps {
        sh "docker push ${params.dockerRegistry}/com.devsoap/nginx-proxy:${params.buildVersion}"	
      }
    }
  }
}
