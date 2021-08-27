pipeline {
  agent {
    node {
      label 'docker-vm'
    }

  }
  stages {
    stage('CheckOut Code') {
      steps {
        git(url: 'https://github.com/razorbach1/dotnet-core-api.git', branch: 'master', changelog: true, poll: true)
      }
    }

  }
}