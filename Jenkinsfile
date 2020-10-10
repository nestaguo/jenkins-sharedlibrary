#!groovy

@Library('jenkinslib') _

def tools = new org.devops.tools()

//hello()

pipeline {
    agent { node { label 'jenkins-master01' } }
    
    options {
        timestamps()
        skipDefaultCheckout()
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'HOURS')
    }
    
    stages{
        
        stage('Get Code'){
            steps{
                timeout(time:5, unit:'MINUTES'){
                    script{
                        println('获取代码')
                    }
                }
            }
            
	    input {
 		message 'can we go?'
		id 'Test1'
  		ok 'Next'
  		submitter 'admin'
  		parameters {
    	            choice choices: ['finished', 'failed'], description: '', name: 'test1'
  		}
	    }	
           
        }
        
        stage('Parallel Stage') {
            failFast true
            parallel{
                stage('Build'){
                    steps{
                        timeout(time:20, unit:'MINUTES'){
                            script{
                                println('应用打包')
                            }
                        }
                    }
                }
                
                stage('CodeScan'){
                    steps{
                        timeout(time:30, unit:'MINUTES'){
                            script{
                                println('代码扫描')

                                tools.PrintMes("This is nesta lib!")
                            }
                        }
                    }
                }
            }
        }
        
    }
    
    post {
    always{
        script{
            println("流水线结束后，经常做的事情")
        }
    }
        
    success{
        script{
            currentBuild.description = "\n 流水线构建成功"
        }
        
    }
    failure{
        script{
            currentBuild.description = "\n 流水线构建失败"
        }
    }
        
    aborted{
        script{
            currentBuild.description = "\n 流水线取消后，要做的事情"
        }
        
    }
    }
}
