node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("christopherrlittle/simplilearndevopsimage")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
         docker.withRegistry( '', 'docker-hub' ) {
            app.push("latest")
         }
    }
    
    stage('Pull image from DockerHub') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        docker.withRegistry( '', 'docker-hub' ) {
            app.pull("latest")
        }
    }
    
    stage('Rebuild image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("christopherrlittle/simplilearndevopsimage")
    }
}
