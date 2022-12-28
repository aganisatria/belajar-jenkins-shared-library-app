pipeline {
    agent none

    environment {
        AUTHOR = "Agani Satria"
        EMAIL = "Aganisatria1@gmail.com"
    }

    stages {
        stage("Prepare") {
            environment {
                APP = credentials("gani_rahasia")
            }

            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Author: ${AUTHOR}")
                echo("Email: ${EMAIL}")
                echo("App User: ${APP_USR}")
                sh('echo "App Password: $APP_PSW" > "rahasia.txt"')
                echo("Start job: ${env.JOB_NAME}")
                echo("Start build: ${env.BUILD_NUMBER}")
                echo("Branch Name: ${env.BRANCH_NAME}")
            }
        }
        stage("Build") {
            agent {
                node {
                    label "linux && java11"
                }
            }
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
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                script{
                    def data = [
                        "firstName": "Agani",
                        "lastName": "Satria"
                    ]

                    writeJSON(file: "data.json", json: data)
                }
                echo("Hello Test")
                sh("chmod +x mvnw")
                sh("./mvnw test")
                echo("Finish Test")
            }
        }
        stage("Deploy") {
            agent {
                node {
                    label "linux && java11"
                }
            }
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