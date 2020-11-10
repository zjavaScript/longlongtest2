pipeline{
    agent none

    options { disableConcurrentBuilds() }

    parameters{
        booleanParam(name: 'CHECKOUT', defaultValue: true, description: '代码检出')
        booleanParam(name: 'BUILD', defaultValue: true, description: '打包')
    }

    stages{
        stage('初始化'){
            agent{label 'master'}
            stages{
                stage('主节点同步'){
                    steps{
                        script{
                            checkout_repository = "${params.CHECKOUT}"
                            build = "${params.BUILD}"
                        }
                    }
                }
            } 
        }
        stage('分发到节点'){
            agent{ label 'web-test-server'}
            stages{
                stage('代码检出'){
                    when{
                        expression { checkout_repository == 'true' }
                    }
                    steps{
                        script{
                            checkout(
                                [$class: 'GitSCM', branches: [[name: '*/master']], 
                                doGenerateSubmoduleConfigurations: false, 
                                extensions: [[$class: 'LocalBranch', localBranch: 'master']],
                                submoduleCfg: [], 
                                userRemoteConfigs: 
                                [
                                    [
                                        credentialsId: '7646d0ee-9484-46b4-b4e9-6f8893aa3f20', 
                                        url: 'git@gitee.com:UWA_TECHNOLOGIES/uwa-answer-next-version.git'
                                        ]
                                    ]
                                ]
                            )
                        }
                    }
                }
                stage('打包发布'){
                    when{
                        expression { build == 'true' }
                    }
                    steps{
                        sh label: '', script: 'sh ${WORKSPACE}/start.sh'
                    }
                }
            }
        }
    }
    post{
        always{
            node('master'){
                emailext body: '$DEFAULT_CONTENT', 
                subject: '$DEFAULT_SUBJECT', to: 'Jenkins.answer@uwa4d.com'
            }
        }
    }
}