#!/usr/bin/env groovy
 
/*
 * Sample Jenkinsfile for Jenkins2 Pipeline
 * from https://github.com/hotwilson/jenkins2/edit/master/Jenkinsfile
 * by wilsonmar@gmail.com 

import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurperClassic
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL
*/
 
try {
	node {
		stage ('Stage 1') {
			echo "BUILD_URL=${env.BUILD_URL}"
		}
		
		stage ('Stage 2' ) {
			def workspace = pwd()
			echo "workspace=${WORKSPACE}"
		}
	} // node
} // try end
catch (exc) {
 err = caughtError
 currentBuild.result = "FAILURE"
 String recipient = 'infra@lists.jenkins-ci.org'
 mail subject: "${env.JOB_NAME} (${env.BUILD_NUMBER}) failed",
         body: "It appears that ${env.BUILD_URL} is failing, somebody should do something about that",
           to: recipient,
      replyTo: recipient,
 from: 'noreply@ci.jenkins.io'
} finally {
 (currentBuild.result != "ABORTED") && node("base") {
     // Send e-mail notifications for failed or unstable builds.
     // currentBuild.result must be non-null for this step to work.
     step([$class: 'Mailer',
        notifyEveryUnstableBuild: true,
        recipients: "Evgenii_Pomnikov@epam.com",
        sendToIndividuals: true])
}

 // Must re-throw exception to propagate error:
 /*
 if (exc) {
     throw exc
 }*/
}
