node {
    try {
        stage('Build') {
            def image = docker.image('node:16-buster-slim')
            try {
                image.inside('-p 3000:3000') {
                    sh 'npm install'
                }
            } catch (Exception e) {
                currentBuild.result = 'FAILURE'
                error("Build failed: ${e.getMessage()}")
            }
        }
        stage('Test') {
            def image = docker.image('node:16-buster-slim')
            try {
                image.inside('-p 3000:3000') {
                sh './jenkins/scripts/test.sh'
                }
            } catch (Exception e){
                currentBuild.result = 'FAILURE'
                error("Tests failed: ${e.getMessage()}")
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        error("Pipeline failed: ${e.getMessage()}")
    }
}