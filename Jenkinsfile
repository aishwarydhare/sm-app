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
      sh 'docker run -p 80:80 --name sm-app myc:latest'
    }
    stage('Docker test'){
      sh 'myfile.sh'
    }
  }
  catch (err) {
    throw err
  }
}

