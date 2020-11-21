#!/usr/bin/env groovy
String daily_cron_string = BRANCH_NAME == "master" ? "@daily" : ""

pipeline {
    agent any

    triggers { cron(daily_cron_string) }

    stages {
        stage('... Environment interrogation ...') {
            steps {
                echo 'Environment:'
                sh "env"
                echo 'Buildah info:'
                sh "buildah info"
            }
        }
        stage('... Running ...') {
            parallel {
                stage ('Jenkins') {
                    steps {
                        ansiColor('xterm') {
                            echo '... Building ...'
                            sh "buildah bud -t tinkerjenkins -f Dockerfile.centos tinkerjenkins"
                            sh "buildah push tinkerjenkins docker://registry.tinker.haus/tinkerjenkins:centos"
                        }
                    }
                }
                stage ('nextcloud') {
                    steps {
                        ansiColor('xterm') {
                            echo '... Building ...'
                            sh "buildah bud -t tinkernextcloud -f Dockerfile tinkernextcloud"
                            sh "buildah push tinkernextcloud docker://registry.tinker.haus/tinkernextcloud:latest"
                        }
                    }
                }
            }
        }
    }
}
