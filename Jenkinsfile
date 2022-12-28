pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("Build") {
            steps {
                script{
                    for(int i = 0; i < 10; i++){
                        echo("Script ${i}")
                    }
                }
                echo("Hello Build")
                sh("chmod +x mvnw")
                sh("./mvnw clean compile test-compile")
                echo("Finish Build")

            }
        }
        stage("Test") {
            steps {
                script{
                    def data = [
                        "firstName": "Agani",
                        "lastName": "Satria"
                    ]

                    writeJSON(file: "data.json", json: data)
                }
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