pipeline {
    agent { label 'JDK_8'}
    options {
        retry(3)
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * ')
    }
    tools {
        jdk 'JAVA_8'
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/asusrepos/game-of-life-july23.git',
                branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh script: 'mvn clean package'
            }
        }
        stage('report') {
             steps {
                junit testResults: '**//surefire-reports/TEST-*.xml'
            }
        }
    }
}