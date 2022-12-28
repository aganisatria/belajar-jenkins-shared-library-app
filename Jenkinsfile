pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("Build") {
            steps {
                echo("Hello Build")
            }
        }
        stage("Test") {
            steps {
                echo("Hello Test")
                sh("error")
            }
        }
        stage("Deploy") {
            steps {
                echo("Hello Deploy")
            }
        }
    }
    post {
        always {
            echo 'I will always love you'
        }
        success {
            echo 'I will always success'
        }
        failure {
            echo 'I will always failure'
        }
        cleanup {
            echo 'I will always cleanup'
        }
    }
}