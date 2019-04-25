node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("webserver")
    }

    stage('Run image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app = docker.image('webserver').withRun("-p 8082:80") { c ->
           sh 'echo Container Built'   
        }
        app.inside {
           sh 'cat /usr/local/apache2/htdocs/index.html'   
        }
    }
}
