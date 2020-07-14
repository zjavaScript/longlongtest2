pipeline {
  agent any
  stages {
    stage('1') {
      parallel {
        stage('1') {
          steps {
            sh 'LS'
          }
        }

        stage('2') {
          steps {
            sh '2'
          }
        }

        stage('3') {
          steps {
            sh '3'
          }
        }

      }
    }

    stage('4') {
      parallel {
        stage('4') {
          steps {
            sh '4'
          }
        }

        stage('5') {
          steps {
            sh '5'
          }
        }

      }
    }

    stage('6') {
      steps {
        sh '6'
      }
    }

  }
}