pipeline {
    agent any
    tools {
        go 'go1.18'
    }
    environment {
        GO118MODULE = 'on'
    }
    stages {
        stage('Compile') {
            steps {
                sh 'go build'
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | bash -s -- -b $GOPATH/bin v1.12.5'
                sh 'golangci-lint run'
            }
        }
        stage('Release') {
            when {
                buildingTag()
            }
            environment {
                GITHUB_TOKEN = credentials('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')
            }
            steps {
                sh 'curl -sL https://git.io/goreleaser | bash'
            }
        }
    }
}
