pipeline {
    agent { label 'JDK_17' }
    triggers { pollSCM('* * * * *') }
    parameters { choice(name: '$MAVEN GOAL', choices: ['package', 'install', 'clean']) }
    stages {
        stage('VCS') {
            steps {
                git branch: 'declarative,'
                    url: 
            }
        }
    }
}