node {
    def server = Artifactory.newServer url: 'http://192.168.23.2:8081/artifactory', username: 'admin', password: '159357V@Clandic' 
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo

    stage ('Clone') {
        git url: 'https://github.com/vaclandic/java_hello.git'
    }

    stage ('Artifactory configuration') {
        rtMaven.tool = "maven" 
        buildInfo = Artifactory.newBuildInfo()
    }

    stage ('Exec Maven') {
        rtMaven.run pom: 'pom.xml', goals: 'compile package', buildInfo: buildInfo
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
    stage ('Build Docker container') {
        sh 'ls -l target'
    }
}
