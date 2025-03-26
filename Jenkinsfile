pipeline {
    agent any // 실행할 Jenkins 에이전트 (any는 아무 노드에서 실행 가능)

    // 환경 변수 설정 (필요 시)
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk' // Java 경로 (Jenkins 서버에 맞게 수정)
    }

    stages {
        // 1. GitHub에서 소스 코드 가져오기
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/aicfo2/publicDeployTest.git',
                    credentialsId: '7bd53990-5792-4eb4-a57d-53d50b773c57' // Jenkins에 설정한 GitHub 토큰 ID
            }
        }

        // 2. 프로젝트 빌드 (Maven 기준)
        stage('Build') {
            steps {
                sh 'chmod +x ./mvnw' // mvnw 실행 권한 부여 (필요 시)
                sh './mvnw clean package -DskipTests' // 테스트 건너뛰고 빌드
            }
        }

        // 3. 테스트 실행
        stage('Test') {
            steps {
                sh './mvnw test' // 단위 테스트 실행
            }
        }

        // 4. 배포 (예: JAR 파일 실행)
        stage('Deploy') {
            steps {
                sh 'java -jar target/demo-0.0.1-SNAPSHOT.jar' // 빌드된 JAR 파일 실행 (실제 배포 방식에 따라 수정)
            }
        }
    }

    // 빌드 후 처리
    post {
        always {
            echo 'Pipeline execution completed!'
        }
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}