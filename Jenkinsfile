#!groovy

/* Only keep the 10 most recent builds. */
properties([[$class: 'BuildDiscarderProperty',
                strategy: [$class: 'LogRotator', numToKeepStr: '10']]])

stage ('Build') {

  node {
    // Checkout
    checkout scm

    // install required bundles
    powershell 'bundle install'

    // build and run tests with coverage
    powershell 'bundle exec rake build spec'

    // Archive the built artifacts
    archive (includes: 'pkg/*.gem')

    // publish html
    publishHTML ([
        allowMissing: false,
        alwaysLinkToLastBuild: false,
        keepAll: true,
        reportDir: 'coverage',
        reportFiles: 'index.html',
        reportName: "RCov Report"
      ])

  }
}
