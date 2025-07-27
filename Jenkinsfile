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
}
