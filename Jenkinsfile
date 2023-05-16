
pipeline {
    agent any
    environment {
      PATH = "$PATH:/tmp/workspace/flutter/bin"
    }
    stages {
        stage('GIT PULL') {
            steps {
                git branch: "main", url: 'https://github.com/mongvaka/test_build_android.git'
            }
        }

        stage('Build') {
            steps {
                sh "flutter doctor -v"
            }
        }
        stage('TEST') {
            steps {
                sh 'flutter test'
            }
        }
        stage('BUILD') {
            steps {
                sh '''
                  #!/bin/sh
                  flutter build apk --debug
                  '''
            }
        }
        stage('DISTRIBUTE') {
            steps {
                appCenter apiToken: 'f9f0ed116d89a9459101f2de56b60bc03d465d93',
                        ownerName: 'sanit.vakch-gmail.com',
                        appName: 'testBuild',
                        pathToApp: 'build/app/outputs/apk/debug/app-debug.apk',
                        distributionGroups: 'AlphaTester'
            }
        }
    }
}