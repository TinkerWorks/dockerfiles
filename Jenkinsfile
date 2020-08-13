#!/usr/bin/env groovy

pipeline {
    agent any

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
