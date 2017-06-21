node {
    git "https://github.com/$GITHUB_ID/example-voting-app.git"
    stage('Build') {
        parallel (
            result: { sh "docker image build -t $DOCKERHUB_ID/voting-result result" },
            worker: { sh "docker image build -t $DOCKERHUB_ID/voting-worker worker" },
            vote: { sh "docker image build -t $DOCKERHUB_ID/voting-vote vote" }
        )
    }
    stage('Test') {
        parallel (
            result: { sh "echo result-test" },
            worker: {sh "echo worker-test"},
            vote: {sh "echo vote-test"}
        )
    }
    stage('Push') {
        withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            sh 'docker login -u $USERNAME -p $PASSWORD'
        }
        parallel (
            result: { sh "docker image push $DOCKERHUB_ID/voting-result" },
            worker: { sh "docker image push $DOCKERHUB_ID/voting-worker" },
            vote: { sh "docker image push $DOCKERHUB_ID/voting-vote" }
        )
    }
    stage('Deploy') {
        sh 'docker-compose up -d'
    }
}
