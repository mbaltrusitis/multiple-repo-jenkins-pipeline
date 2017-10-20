pipeline {
  agent any
  stages {
    stage('Checking out first') {
      steps {
        sh 'mkdir -p deps/python-requests deps/python-pelican'
        dir('deps') {
          dir('python-requests') {
            git(url: 'https://github.com/requests/requests.git', branch: 'master')
          }
        }
      }
    }
  }
}
