pipeline {
    agent none

    environment {
        AUTHOR = "Agani Satria"
        EMAIL = "Aganisatria1@gmail.com"
    }

    // triggers {
    //     cron("*/5 * * * *")
    // }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "", description: "Tell me about tou?")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ["Instagram", "Facebook", "Twitter"], description: "Which social media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit:'MINUTES')
    }

    stages {
        stage("OS Setup"){
            matrix{
                axes{
                    axis{
                        name "OS"
                        values "linux", "windows", "mac"
                    }
                    axis{
                        name "ARC"
                        values "32", "64"
                    }
                }
                stages{
                    stage("OS Setup"){
                        agent{
                            node{
                                label "linux && java11"
                            }
                        }
                        steps{
                            echo "Setup ${OS} ${ARC}"
                        }
                    }
                }
            }
        }

        stage("Preparation"){
            failFast true
            parallel {
                stage("Prepare java"){
                    agent{
                        node{
                            label "linux && java11"
                        }
                    }
                    steps{
                        echo "Prepare java"
                        sleep(5)
                    }
                }
                stage("Prepare maven"){
                    agent{
                        node{
                            label "linux && java11"
                        }
                    }
                    steps{
                        echo "Prepare maven"
                        sleep(5)
                    }
                }
            }
        }

        stage("Parameter"){
            agent{
                node{
                    label "linux && java11"
                }
            }
            steps {
                echo("Hello: ${params.NAME}")
                echo("Your description: ${params.DESCRIPTION}")
                echo("Your social media: ${params.SOCIAL_MEDIA}")
                echo("Need to deploy: ${params.DEPLOY}")
                echo("Your secret is: ${params.SECRET}")
            }
        }

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
            input {
                message "Can we Deploy?"
                ok "Yes, of course."
                submitter "gani, aganisatria"
                parameters {
                    choice(name: 'TARGET_ENV', choices: ['DEV', 'QA', 'PROD'], description: "We will deploy to?")
                }
            }
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Deploy to ${TARGET_ENV}")

            }
        }
        stage("Release") {
            when{
                expression{
                    return params.DEPLOY
                }
            }
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo "Release it"
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