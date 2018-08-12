pipeline {
    agent any
    stages {
        stage ('Build') {
            steps {
                git 'https://github.com/interview-project/spring-petclinic.git'
                sh './mvnw package'
            }
        }
        stage ('Publish') {
            steps {
                nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '.jar', filePath: 'target/spring-petclinic-2.0.0.BUILD-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'spring-petclinic', groupId: 'org.springframework.samples', packaging: 'petclinic', version: "${env.BRANCH_NAME}-${currentBuild.number}"]]]
            }
        }
    }
}