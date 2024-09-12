pipeline {
  agent {
    docker {
      image 'ubuntu'
    }

  }
  stages {
    stage('checkout') {
      steps {
        dir(path: 'https://github.com/umabawania/customs-addons.git')
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t odoo16:latest .'
      }
    }

    stage('Login to ECR') {
      steps {
        sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/g1t1m4r7'
      }
    }

    stage('pushing to ECR') {
      steps {
        sh 'docker tag odoo16:latest public.ecr.aws/g1t1m4r7/odoo16:latest'
      }
    }

    stage('pushing image') {
      steps {
        sh 'docker push public.ecr.aws/g1t1m4r7/odoo16:latest'
      }
    }

  }
}