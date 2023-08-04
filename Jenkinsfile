pipeline {
    agent { label 'JDK_17' }
    triggers { pollSCM('* * * * *') }
    parameters { choice(name: 'MAVEN GOAL', choices: ['package', 'install', 'clean']) }
    stages {
        stage('VCS') {
            steps {
                git branch: 'declarative',
                    url: 'https://github.com/2023August/spring-petclinic.git'
            }
        }
        stage('package') {
            steps {
                sh '$MAVEN GOAL' 
            }
        }
    }
}