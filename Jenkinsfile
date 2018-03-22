node {
    def server = Artifactory.newServer url: 'http://192.168.23.2:8081/artifactory', username: 'admin', password: '159357V@Clandic' 
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo

    stage ('Clone') {
        git url: 'https://github.com/vaclandic/java_hello.git'
    }

    stage ('Artifactory configuration') {
//        rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
//        rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
//        rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
        buildInfo = Artifactory.newBuildInfo()
    }

    stage ('Exec Maven') {
        rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
}
