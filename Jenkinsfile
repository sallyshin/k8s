node {
  stage('========== Clone repository ==========') {
    checkout scm
  }
  stage('========== Build image ==========') {
    app = docker.build("ellisjoe611/grooming") 
  }
  stage('========== Push image ==========') {
    docker.withRegistry('https://registry.hub.docker.com', 'ellisjoe611') {
      app.push("${env.BUILD_NUMBER}")
      app.push("latest") 
    }
  }
}
