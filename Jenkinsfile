node {
    stage('Build') {
        git "https://github.com/$GITHUB_ID/example-voting-app.git"
        parallel (
            result: { sh "docker image build -t $DOCKERHUB_ID/voting-result result" },
            worker: { sh "docker image build -t $DOCKERHUB_ID/voting-worker worker" },
            vote: { sh "docker image build -t $DOCKERHUB_ID/voting-vote vote" }
        )
    }
    stage('Test') {
        parallel (
            phase1: { sh "echo p1; sleep 20s; echo phase1" },
            phase2: { sh "echo p2; sleep 40s; echo phase2" }
        )
    }
    stage('Push') {
        parallel (
            phase1: { sh "echo p1; sleep 20s; echo phase1" },
            phase2: { sh "echo p2; sleep 40s; echo phase2" }
        )
    }
}
