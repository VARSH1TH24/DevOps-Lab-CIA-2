
pipeline {
    agent any

    stages {
        stage('Build and Test') {
            steps {
                dir('C:\\Users\\snucse\\Downloads\\Student-Starter\\Student-Starter') {
                    bat '"C:\\Tools\\apache-maven-3.10.0\\bin\\mvn.cmd" clean test'
                }
            }
        }

        stage('Package') {
            steps {
                dir('C:\\Users\\snucse\\Downloads\\Student-Starter\\Student-Starter') {
                    bat '"C:\\Tools\\apache-maven-3.10.0\\bin\\mvn.cmd" package'
                }
            }
        }
    }

    post {
        always {
            bat '''
                if not exist reports mkdir reports
                if not exist artifacts mkdir artifacts
                if exist "C:\\Users\\snucse\\Downloads\\Student-Starter\\Student-Starter\\course-registration-app\\target\\surefire-reports\\TEST-*.xml" copy /Y "C:\\Users\\snucse\\Downloads\\Student-Starter\\Student-Starter\\course-registration-app\\target\\surefire-reports\\TEST-*.xml" reports\\
                if exist "C:\\Users\\snucse\\Downloads\\Student-Starter\\Student-Starter\\course-registration-app\\target\\*.jar" copy /Y "C:\\Users\\snucse\\Downloads\\Student-Starter\\Student-Starter\\course-registration-app\\target\\*.jar" artifacts\\
            '''

            junit(
                testResults: 'reports/TEST-*.xml',
                allowEmptyResults: false
            )

            archiveArtifacts(
                artifacts: 'artifacts/*.jar',
                allowEmptyArchive: false
            )
        }
    }
}
