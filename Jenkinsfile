pipeline {
    agent { label 'MAVEN_JDK' }
    triggers { pollSCM('* * * * *') }
    parameters { choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean']) }
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
                sh  "mvn ${params.MAVEN_GOAL}"
            }
        }
       stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.1.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/TEST-*.xml'                 
            }
        }
    }
} 


