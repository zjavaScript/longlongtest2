pipeline {
  agent any
  stages {
    stage('111') {
      steps {
        archiveArtifacts(artifacts: '1111222', allowEmptyArchive: true, caseSensitive: true, followSymlinks: true, defaultExcludes: true, excludes: '345', fingerprint: true, onlyIfSuccessful: true)
      }
    }

  }
}