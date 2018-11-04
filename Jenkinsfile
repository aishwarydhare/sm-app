node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Build Docker'){
     sh 'docker build -t myc .'
    }
    stage('Docker run'){
      sh 'docker run -p -d 82:80 -d --name sm-app myc:latest'
    }
    stage('Docker test'){
      sh 'sh myfile.sh'
    }
    stage('Clean Docker test'){
      sh 'docker stop sm-app'
      sh 'docker container rm sm-app'
      sh 'docker image rm myc'
    }
  }
  catch (err) {
    throw err
    stage('Clean Docker test'){
      sh 'docker stop sm-app'
      sh 'docker container rm sm-app'
      sh 'docker image rm myc'
    }
  }
}

