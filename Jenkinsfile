pipeline {
  agent any

  stages {
    stage('Checkout') {
        options {
            retry(3)
        }
        steps {
            //Checkout new source code
            checkout([$class: 'GitSCM',
            branches: [[name: "main"]],
            submoduleCfg: [],
            userRemoteConfigs: [[url: 'https://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@github.com/mongvaka/test_build_android.git']]])
        }
    }
    stage('Clean') {
        steps {
            sh './gradlew clean'
        }
    }
    stage('Build') {
        steps {
            sh './gradlew assembleDevDebug'

            archiveArtifacts '**/*.apk'
        }
    }
    stage('Test') {
        steps {
          // Compile and run the unit tests for the app and its dependencies
          sh './gradlew testDevDebugUnitTestCoverage'

          // Analyse the test results and update the build result as appropriate
          junit(
              allowEmptyResults: false,
              testResults: '**/build/test-results/**/*.xml'
          )
        }
    }

  }


}
