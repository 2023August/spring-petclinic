pipeline {
    agent { label 'JDK_17' }
    triggers { pollSCM('* * * * *') }
    parameters { choice(name: 'MAVEN GOAL', choices: ['package', 'install', 'clean']) }
    stages {
        stage('VCS') {
            steps {
                git url: 'https://github.com/2023August/spring-petclinic.git',
                    branch: 'declarative'
            }
        }
        stage('package') {
            tools { jdk 'JDK_17' }
            steps {
                sh '$MAVEN GOAL' 
            }
        }
    }
}


