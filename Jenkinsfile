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
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SONAR_CLOUD_TOKEN') {
                sh 'mvn clean verify sonar:sonar -Dsonar.token=faa4fa0f55ea846e40e39782b8fd823fa0eccdbb -Dsonar.organization=springpetclinic11 -Dsonar.projectKey=springpetclinic11'
                }
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


