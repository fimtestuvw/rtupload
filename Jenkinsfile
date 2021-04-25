node {

    stage('Clone') {
      // Clones the repository from the current branch name
        cleanWs()
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

        for (int i = 0 ; i < buildInfo.getArtifacts().size() ; i++) {
            def localPath = buildInfo.getArtifacts()[i].getLocalPath()
            println(localPath)
            def remotePath = buildInfo.getArtifacts()[i].getRemotePath()
            println(remotePath)
            def md5 = buildInfo.getArtifacts()[i].getMd5()
            println(md5)
            def sha1 = buildInfo.getArtifacts()[i].getSha1()
            println(sha1)
            print('+++++++++++++++++++')
            // echo remotePath
        }

        server.publishBuildInfo buildInfo
    }



    stage('Download from Jfrog'){
        def server = Artifactory.server 'auditsg'
        def downloadSpec = readFile 'downloadSpec.json'
        sh 'mkdir downloads'
        dir('downloads'){
            sh 'pwd'
            sh 'hostname'
            def buildInfo = server.download spec: downloadSpec

            for (int i = 0 ; i < buildInfo.getArtifacts().size() ; i++) {
                def localPath = buildInfo.getArtifacts()[i].getLocalPath()
                println(localPath)
                def remotePath = buildInfo.getArtifacts()[i].getRemotePath()
                println(remotePath)
                def md5 = buildInfo.getArtifacts()[i].getMd5()
                println(md5)
                def sha1 = buildInfo.getArtifacts()[i].getSha1()
                println(sha1)
                print('+++++++++++++++++++')
                // echo remotePath
            }
        }

    }
}
