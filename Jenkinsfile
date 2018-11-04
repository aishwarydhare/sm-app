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
      sh 'myfile.sh'
    }
    stage('Clean Docker test'){
      sh 'docker rmi sm-app'
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t aishwarydhare/docker-react -f Dockerfile.dev .'
        sh 'docker run aishwarydhare/docker-react npm run test -- --coverage'
      }
    }
  }
  catch (err) {
    throw err
  }
}