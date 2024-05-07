// Filename: Jenkinsfile
node {
  def GITREPOREMOTE = "https://github.com/biswarup-nandi/jenkins-cloudformation.git"
  def GITBRANCH     = "main"
  def AWSCLIPATH     = "/usr/local/bin"

  stage('Checkout') {
    git branch: GITBRANCH, url: GITREPOREMOTE
  }
  stage('Validation') {
    sh """#!/bin/bash
          ls
          aws --version
          whereis aws
       """
  }
}