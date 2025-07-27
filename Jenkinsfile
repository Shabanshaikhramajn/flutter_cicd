pipeline {
    agent any

    environment {
        PATH = "/home/shaban/flutter/bin:$PATH"
        ANDROID_SDK_ROOT = "/home/shaban/Android"
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
        GRADLE_USER_HOME = "$HOME/.gradle"
    }

    stages {
        stage('Flutter Doctor (Optional)') {
            steps {
                sh 'flutter doctor -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'flutter pub get'
            }
        }

        stage('Build APK') {
            steps {
                sh 'flutter build apk --release'
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'build/app/outputs/flutter-apk/app-release.apk'
            }
        }
    }
}
