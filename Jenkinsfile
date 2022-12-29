@Library("belajar-jenkins-shared-library@master") _

import aganisatria.jenkins.Output;

pipeline{
    agent any
    stages{
        stage("Hello Groovy"){
            steps{
                script{
                    def coba = new Output()
                    coba.hello("Groovy")
                }
            }
        }
        stage("Hello World"){
            steps{
                script{
                    hello.world()
                }
            }
        }
    }
}