pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("Hello") {
            steps {
                echo("Hello Pipeline")
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