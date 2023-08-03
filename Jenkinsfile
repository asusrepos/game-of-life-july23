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
            choice(name: "GOAL", choices: ['package', 'install', 'clean package', 'clean install'], description: 'thi is maven goal')
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
                sh script: "mvn ${params.GOAL}"
            }
        }
        stage('report') {
             steps {
                junit testResults: '**//surefire-reports/TEST-*.xml'
            }
        }
    }
}  
        