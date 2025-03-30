pipeline {
    agent any
    tools {
        jdk 'JDK11' // Jenkins 설정에서 유효한 도구 이름 사용
    }
    stages {
        stage('Test') {
            steps {
                sh 'java -version'
            }
        }
    }
}
