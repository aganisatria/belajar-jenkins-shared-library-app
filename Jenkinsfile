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
                sleep(10)
                echo("Hello Build2")

            }
        }
        stage("Test") {
            steps {
                echo("Hello Test")
                sleep(10)
                echo("Hello Test2")
            }
        }
        stage("Deploy") {
            steps {
                echo("Hello Deploy")
                sleep(10)
                echo("Hello Deploy2")

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