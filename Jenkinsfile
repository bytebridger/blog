pipeline {
  agent any
  stages {
    stage('checkout-code') {
      parallel {
        stage('checkout-code') {
          steps {
            git(url: 'https://github.com/b-husein/blog', branch: 'main')
          }
        }

        stage('Sample code') {
          steps {
            sh 'mkdir "Hi there. This is just a test."'
          }
        }

      }
    }

  }
}