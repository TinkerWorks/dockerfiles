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
        stage('Build containers') {
            steps {
                ansiColor('xterm') {
                    echo '... Building ...'
                    sh "buildah bud -t tinkerjenkins -f Dockerfile.centos tinkerjenkins"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                ansiColor('xterm') {
                    echo '... Building ...'
                    sh "buildah push tinkerjenkins docker://registry.tinker.haus/tinkerjenkins:centos"
                }
            }
        }
    }
}
