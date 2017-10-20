pipeline {
  agent any
  stages {
    stage('Checking out first') {
      steps {
        sh 'mkdir -p deps/python-requests deps/python-pelican'
        dir('deps') {
          dir('python-requests') {
            checkout resolveScm(source: git('https://github.com/requests/requests.git'), targets: [BRANCH_NAME, 'master'])
          }
        }
        sh 'echo "Great success!"'
      }
    }
  }
}
