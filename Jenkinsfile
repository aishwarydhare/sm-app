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
     sh 'sudo docker build -t myc .'
    }
    stage('Docker run'){
      sh 'sudo docker run -p 82:80 --name sm-app myc:latest'
    }
    stage('Docker test'){
      sh 'sh myfile.sh'
    }
    stage('Clean Docker test'){
      sh 'sudo docker stop sm-app'
      sh 'sudo docker container rm sm-app'
      sh 'sudo docker image rm myc'
    }
  }
  catch (err) {
    throw err
  }
}
