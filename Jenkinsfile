library identifier: "pipeline-library@v1.4",
retriever: modernSCM(
  [
    $class: "GitSCMSource",
    remote: "https://github.com/redhat-cop/pipeline-library.git"
  ]
)
pipeline {
  agent {
    label 'master'
  }
stages {
stage("Sync") {
  steps {
  script {
  sh """
  ls -R 
  """
  retry(5) {
  try {
  openshift.withCluster() {
    openshift.withProject("") {
      openshift.raw("apply","-Rf","non-prod","--loglevel=8")
      }
    }
  } catch(Exception e) {
      sleep 5
      error "apply failed"
    }
  }
}
}
}
}
}