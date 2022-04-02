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
                        stageName = "$CPU"
                        // stageName stage
                        jobs[stageName] = {
                            stage('ParallelBuild') {
                                node {
                                    withEnv(["CPU=${CPU}"]) {
                                        // checkout Jenkinsfilescripts/
                                        //git branch: "config-rtostest",
                                        //    url: "ssh://psp.sdlc.rd.realtek.com:29418/sdlc/rtos/jenkins"
                                        //pipelineAsCode.parallelStages()
                                        stage("A") {
                                            print "A"
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
