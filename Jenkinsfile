node {
 	// Clean workspace before doing anything
    deleteDir()
	

    try {
		properties([
			pipelineTriggers([
				cron('*/5 * * * *')
			]),
			buildDiscarder(logRotator(daysToKeepStr: '3', numToKeepStr: '100', artifactNumToKeepStr: '1'))
		])
		
		stage ('Clone') {
			checkout scm
		}
		stage ('Build') {
			sh "echo 'shell scripts to build project...'"
		}
		stage ('Tests') {
			parallel 'static': {
				sh "echo 'shell scripts to run static tests...'"
			},
			'unit': {
				sh "echo 'shell scripts to run unit tests...'"
			},
			'integration': {
				sh "echo 'shell scripts to run integration tests...'"
			}
		}
		stage ('Deploy') {
			sh "echo 'shell scripts to deploy to server...'"
		}
		
        
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
