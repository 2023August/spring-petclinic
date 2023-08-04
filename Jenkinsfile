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
            steps {
                tools { 
                    jdk 'JDK_17' 
                    }
                sh '$MAVEN GOAL' 
            }
        }
    }
}


