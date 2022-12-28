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
                sh("./mvnw clean compile test-compile")
                echo("Finish Build")

            }
        }
        stage("Test") {
            steps {
                echo("Hello Test")
                sh("./mvnw test")
                echo("Finish Test")
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