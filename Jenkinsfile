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
                                node("win01") {
                                    withEnv(["CPU=${CPU}"]) {
                                        // checkout Jenkinsfilescripts/
                                        git branch: "main",
                                            url: "https://github.com/reyzheng/paralleljob.git"
                                        //pipelineAsCode.parallelStages()
                                        stage("A") {
                                            print "A"
                                        }
                                        stage("B") {
                                            print "B"
                                        }
                                        stage("C") {
                                            print "C"
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
