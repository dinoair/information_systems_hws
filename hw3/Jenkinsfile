node {
    stage('git clone') {
        git branch: 'main',
            url: 'https://github.com/dinoair/information_systems_hws/hw3/'
            
    }
    stage('build') {
        sh 'mvn -f java/pom.xml clean verify'
    }
    stage('test') {
        sh 'mvn -f java/pom.xml test'
    }
    stage('sonar_qube') {
        def scannerHome = tool 'MySonar';
        withSonarQubeEnv('MySonar') {
            sh "${scannerHome}/bin/sonar-scanner \
            -Dsonar.projectKey=pipeline \
            -Dsonar.sources=java/src/main \
            -Dsonar.tests=java/src/test \
            -Dsonar.java.binaries=java/target/classes \
            -Dsonar.junit.reportPaths=java/target/surefire-reports \
            -Dsonar.coverage.jacoco.xmlReportPaths=java/target/site/jacoco/jacoco.xml"
        }
    }
    stage('allure') {
        allure([
                includeProperties: false,
                jdk: '',
                properties: [],
                reportBuildPolicy: 'ALWAYS',
                results: [[path: 'java/target/allure-results']]
            ])
    }
    stage('deploy') {
            sh 'ansible-playbook deploy/playbook.yml --become --user=USER --become-user=root --become-method=sudo'
        }
    }
}
