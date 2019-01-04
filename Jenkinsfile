node {
    def app
    def GIT_COMMIT_HASH
    def shortGitCommit

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("breeze-nginx")
    }

    stage('Find GIT Hash to Tag Image') {
        GIT_COMMIT_HASH = sh(script: "git log -n 1 --pretty=format:'%H'", returnStdout: true)
        shortGitCommit = GIT_COMMIT_HASH[0..6]
    }

    stage('Push image') {
        sh('$(/usr/local/bin/aws ecr get-login --no-include-email --region us-east-1)')
        
        docker.withRegistry('https://291890047404.dkr.ecr.us-east-1.amazonaws.com') {
            app.push("${shortGitCommit}")
            app.push("latest")
        }
    }
}
