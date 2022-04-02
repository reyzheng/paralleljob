def CPUList = ["arm", "mips"]
pipeline {
    agent any
    stages {
        // pre-requisite stage
        stage('Parallel') {
            steps {
                script {
                    def jobs = [:]
                    for (int i = 0; i < CPUList.size(); i++) {
                        def CPU = CPUList[i]
                        def stageName = "$CPU"
                        // stageName stage
                        jobs[stageName] = {
                            stage(stageName) {
                                node("win") {
                                    //skipDefaultCheckout(false)
                                    // 要自行設定dir, 靠agent的Number of executors不可靠
                                    dir(stageName) {
                                        withEnv(["CPU=${CPU}"]) {
                                            // 要自己重新checkout pipeline again
                                            git branch: "main",
                                                url: "https://github.com/reyzheng/paralleljob.git"
                                            stage("A") {
                                                print "A"
                                                writeFile(file: "a.txt", text: "aaa")
                                                sleep(10)
                                            }
                                            stage("B") {
                                                print "B"
                                                sleep(10)
                                            }
                                            stage("C") {
                                                print "C"
                                                sleep(10)
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                    parallel jobs
                }
            }
        }
        /*
        stage("OutsideParallel") {
            steps {
                script {
                    pipelineAsCode.standaloneStages()
                }
            }
        }
        */
    }
}
