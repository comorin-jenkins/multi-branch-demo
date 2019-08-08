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
     agent any
     stages {
          stage("checkout"){
              steps {
                 checkout scm
              }
          }
          stage("result") {
              steps {
                  sh "./script.sh"
              }
          }
       
          stage("deploy branch feature") {
              when { branch 'feature/*' }
              steps {
                echo "deployed feature branch"
              }
          }
       
          stage("deploy branch feature") {
              when { branch 'develop' }
              steps {
                echo "deployed develop branch"
              }
          }
       
          stage("deploy branch feature") {
              when { branch 'master' }
              steps {
                echo "deployed master branch"
              }
          }
       
          stage("deploy branch feature") {
              when { buildingTag() }
              steps {
                echo "deployed tag"
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
