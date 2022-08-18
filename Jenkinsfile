pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'python:2.7.16-slim'
          args '--user root'
        }

      }
<<<<<<< HEAD
      stage('Unit Test'){
          agent{
            docker{
              image 'python:2.7.16-slim'
              args '--user root'
            }
          }
          steps{
            echo 'Running Unit Tests on vote app'
            dir('vote'){
              sh 'pip install -r requirements.txt'
              sh 'nosetests -v'
            }
          }
      }
      stage('Docker BnP'){
          agent any
          steps{
            echo 'Packaging vote app with docker'
            script{
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                  def voteImage = docker.build("neatleygit/vote:v${env.BUILD_ID}", "./vote")
                  voteImage.push()
                  voteImage.push("dev")
	          voteImage.push("latest")
              }
            }
          }
      }
=======
      steps {
        echo 'Compiling vote app'
        dir(path: 'vote') {
          sh 'pip install -r requirements.txt'
        }
>>>>>>> 3f79fa63d24269d422dab09e7adddc2ebbba3026

      }
    }

    stage('Unit Test') {
      agent {
        docker {
          image 'python:2.7.16-slim'
          args '--user root'
        }

      }
      steps {
        echo 'Running Unit Tests on vote app'
        dir(path: 'vote') {
          sh 'pip install -r requirements.txt'
          sh 'nosetests -v'
        }

      }
    }

    stage('Docker BnP') {
      agent any
      steps {
        echo 'Packaging vote app with docker'
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def voteImage = docker.build("neatley/vote:v${env.BUILD_ID}", "./vote")
            voteImage.push()
            voteImage.push("dev")
            voteImage.push("latest")
          }
        }

      }
    }

  }
  post {
    always {
      echo 'Pipeline for vote is complete..'
    }

  }
}