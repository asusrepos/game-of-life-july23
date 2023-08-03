pipeline {
    agent { label 'JDK_8'}
    options {
        retry(3)
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JAVA_8'
    }
    parameters {
            choice(name: GOAL, choices: ['package', 'install', 'clean install', 'clean install'])
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
     post {
         success {
         mail subject: 'has completed with success',
        body: 'your project is effective \n build url ${BUILD_URL}',
          to: 'all@qt.com'
        }
         failure {
         mail subject: 'has completed with failure',
         body: 'your project is defective \n build url ${BUILD_URL}',
         to: 'all@qt.com'
        }
    }
}