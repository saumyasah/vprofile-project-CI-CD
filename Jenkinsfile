pipeline {
    agent any
    tools {
        maven "MAVEN3.9"
        jdk "JDK17"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin123'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.15.66'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war' // archive anything with ends with '**/*.war'. You can see it in any job which was created successfully>console output> workspaces> click on the link and see all the data
                }
            }
        }

        stage('Test'){
            steps {
                sh 'mvn test' // this will run the unit test and will generate unit tests which will later upload to sonarQube
            }
        }

        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle' // code analysis tool which will check any errors in the code and will suggest best practices and vulnerabilties
            }
        }
    }
}
