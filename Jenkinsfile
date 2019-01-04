node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("getintodevops/hellonode")
    }

    stage('Test image') {
        /* Test steps if any */
    }

    stage('Push image') {
        docker.withRegistry('https://291890047404.dkr.ecr.us-east-1.amazonaws.com') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
