node {

    stage('Clone') {
      // Clones the repository from the current branch name
        def repoUrl= 'https://github.com/fimtestuvw/rtupload'
        def branchName = 'main'
        git branch: branchName,  url: repoUrl


    }

    stage('Upload to Jfrog'){
        def server = Artifactory.server 'auditsg'
        def uploadSpec = readFile 'uploadSpec.json'
        def buildInfo = server.upload spec: uploadSpec
        sh 'ls -ltr'
        println('------------')
        print(buildInfo)
        println('-------------')
        if (buildInfo.getArtifacts().size() > 0) {
            def localPath = buildInfo.getArtifacts()[0].getLocalPath()
            println(localPath)
            def remotePath = buildInfo.getArtifacts()[0].getRemotePath()
            println(remotePath)
            def md5 = buildInfo.getArtifacts()[0].getMd5()
            println(md5)
            def sha1 = buildInfo.getArtifacts()[0].getSha1()
            println(sha1)
            print('+++++++++++++++++++')
            echo remotePath
        }

        // server.publishBuildInfo buildInfo
    }
}
