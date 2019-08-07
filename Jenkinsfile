void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/comorin-jenkins/multi-branch-demo.git"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
pipeline {
     agent {label 'build'}
     stages {
          stage("checkout"){
              steps {
                 checkout scm
              }
          }
          stage("result") {
              steps {
                  sh "script.sh"
              }
          }
      }
      post {
         success {
               setBuildStatus("Build succeeded", "SUCCESS");
         }
         failure {
              setBuildStatus("Build failed", "FAILURE");
         }
     }
}
