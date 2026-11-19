node {
    def PROJECT_DIR = '.'

    stage('Checkout') {
        checkout scm
    }

    stage('Build Information') {
        echo "Build Number: ${env.BUILD_NUMBER}"
        echo "Workspace: ${env.WORKSPACE}"
    }

    stage('Clean') {
        dir(PROJECT_DIR) {
            bat 'mvn clean'
        }
    }

    stage('Install') {
        dir(PROJECT_DIR) {
            bat 'mvn install'
        }
    }

    stage('Test') {
        dir(PROJECT_DIR) {
            bat 'mvn test'
        }
    }

    stage('Package') {
        dir(PROJECT_DIR) {
            bat 'mvn package'
        }
    }

    stage('Verify Artifact') {
        dir(PROJECT_DIR) {
            bat 'dir target'
            bat 'if not exist target\\bloodbank.war exit /b 1'
        }
    }

    stage('Archive Artifact') {
        dir(PROJECT_DIR) {
            archiveArtifacts artifacts: 'target/bloodbank.war',
                             fingerprint: true
        }
    }
}
