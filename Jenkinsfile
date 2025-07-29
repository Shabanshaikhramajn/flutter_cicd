pipeline {
  agent any

  environment {
    PATH = "/opt/flutter/bin:$PATH"
    ANDROID_SDK_ROOT = "/home/shaban/Android"
    JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
  }

  stages {
    stage('Flutter Doctor') {
      steps {
        sh '/opt/flutter/bin/flutter doctor -v'
      }
    }

    stage('Install dependencies') {
      steps {
        sh '/opt/flutter/bin/flutter pub get'
      }
    }

    stage('Build APK') {
      steps {
        sh '/opt/flutter/bin/flutter build apk --release'
      }
    }

    stage('Archive APK') {
      steps {
        archiveArtifacts artifacts: 'build/app/outputs/flutter-apk/app-release.apk'
      }
    }
  }

  post {
    success {
      emailext(
        subject: "Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """Hello,

The Jenkins build succeeded.

You can find the attached APK file.

Build details: ${env.BUILD_URL}

Best,
Jenkins""",
        to: 'shabanshaikh7234@gmail.com',    // Change to your email or list
        attachmentsPattern: 'build/app/outputs/flutter-apk/app-release.apk'
      )
    }
    failure {
      emailext(
        subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: "The Jenkins build failed. Please check: ${env.BUILD_URL}",
        to: 'shabanshaikh7234@gmail.com'    // Change to your email or list
      )
    }
  }
}
