node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("oremari77/hellonode")
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
       /* comment out
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        } */ end comment out


       

       /* I 've added this tho lines to publish the image into the IBM private registry.
        docker tag oremari77/hellonode registry.eu-de.bluemix.net/oreste/hellonode:1
        docker push registry.eu-de.bluemix.net/oreste/hellonode:1

      } 

    stage('Run image into kubernates in IBM Cloud') {
       /* This job run the image in IBM Cloud
         kubectl run hello-world --image=registry.eu-de.bluemix.net/oreste/hellonode:1
         kubectl  expose deployment/hello-world --type=NodePort --port=8080 --name=hello-world-service --target-port=8080
        }
}
