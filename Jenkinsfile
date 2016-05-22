node {
	checkoutStage()
	dockerStage("jenkins-instance", "monochromata/jenkins")
}

def checkoutStage() {
	stage "Checkout"
	git url: "https://github.com/jACT-RTeam/jactr-build.git"
}

def dockerStage(String project, String repository) {
	stage name: project, concurrency: 1
	withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker.hub.credentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USER']]) {
		sh '''cd '''+project+''' \
				&& docker build \
				   --pull \
				   --tag '''+repository+''':latest \
				   . \
				&& docker login \
				   --username=DOCKER_HUB_USER \
				   --password=$DOCKER_HUB_PASSWORD \
				&& docker push '''+repository
	}
}