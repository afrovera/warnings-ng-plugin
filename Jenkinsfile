pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
} }
    stages {
        stage('Spin-up Warnings') {
            steps {
                sh 'mvn -B -DskipTests clean verify checkstyle:checkstyle pmd:pmd findbugs:findbugs'
} }
        stage("OWASP Dependency Checks") {
            steps {
                dependencyCheckAnalyzer datadir: '', hintsFile: '',
 includeHtmlReports: false, includeCsvReports: false, includeJsonReports: false, isAutoupdateDisabled: false,
includeVulnReports: false, outdir: '', scanpath: 'src',
skipOnScmChange: false, skipOnUpstreamChange: false, suppressionFile: '',
zipExtensions: ''
} }
}
    post {
        always {
            recordIssues enabledForFailure: true, tool: mavenConsole(),
referenceJobName: 'Plugins/warnings-ng-plugin/master'
            recordIssues enabledForFailure: true, tool: checkStyle(pattern:
'target/test-classes/io/jenkins/plugins/analysis/warnings/checkstyle.xml'),
sourceCodeEncoding: 'UTF-8', referenceJobName: 'Plugins/warnings-ng-plugin/master'
            recordIssues enabledForFailure: true, tools: [java(), javaDoc()],
sourceCodeEncoding: 'UTF-8', referenceJobName: 'Plugins/warnings-ng-plugin/master'
recordIssues enabledForFailure: true, tool: pmdParser(pattern:
'target/test-classes/io/jenkins/plugins/analysis/warnings/recorder/module-
filter/pmd.xml'), sourceCodeEncoding: 'UTF-8', referenceJobName: 'Plugins/warnings-
ng-plugin/master'
            recordIssues enabledForFailure: true, tool: spotBugs(pattern:
'target/test-classes/io/jenkins/plugins/analysis/warnings/spotbugsXml.xml'),
sourceCodeEncoding: 'UTF-8', referenceJobName: 'Plugins/warnings-ng-plugin/master'
            recordIssues enabledForFailure: true, tool: cpd(pattern:
'target/cpd.xml'), sourceCodeEncoding: 'UTF-8', referenceJobName: 'Plugins/warnings- ng-plugin/master'
            recordIssues enabledForFailure: true, tool:
dependencyCheckPublisher canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
} }
}
