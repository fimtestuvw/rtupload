node {

    stage('Clone') {
      // Clones the repository from the current branch name
        def repoUrl= 'https://github.com/fimtestuvw/rtupload'
        def branchName = 'main'
        git branch: branchName, credentialsId: 	gitCredentials, url: repoUrl


    }

    stage('Upload to Jfrog'){
        def server = Artifactory.server 'auditsg'
        def uploadSpec = readFile 'uploadSpec.json'
        def buildInfo = server.upload spec: uploadSpec

        if (buildInfo.getArtifacts().size() > 0) {
            def localPath = buildInfo.getArtifacts()[0].getLocalPath()
            def remotePath = buildInfo.getArtifacts()[0].getRemotePath()
            def md5 = buildInfo.getArtifacts()[0].getMd5()
            def sha1 = buildInfo.getArtifacts()[0].getSha1()
            echo remotePath
        }

        server.publishBuildInfo buildInfo
    }
}
