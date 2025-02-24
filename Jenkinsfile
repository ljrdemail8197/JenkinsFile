pipeline{
    agent any
    options {
       //retry (3)
    //timeout(time:3,unit:"SECONDS")
      parallelsAlwaysFailFast()
      timestamps()
      disableConcurrentBuilds(abortPrevious:true)
      buildDiscarder(logRotator(numToKeepStr:'10'))
      skipDefaultCheckout()
    }
    //  triggers {
    //     cron('* * * * *')
        //triggers{ cron('H H(9-16)/2 * * 1-5') }
    //}
    environment{
        CC="clang"
        SERVICE_CREDS =credentials('0a46c8cc-ec16-45b9-983b-b1c52e02f8c9')
       
    }
    stages {
        stage("git clone") {      
            steps{        
                script {
                
                env.abc = currentBuild.durationString.split("and counting")[0]
                clearWs()
                sh 'ls -la'
                checkout scm
                sh 'ls -la'
                
                echo "#############Build USER########################"
                wrap([$class:'BuildUser']) {
                    echo "${BUILD_USER}"
                }
                sh '''
                echo "job name: ${JOB_NAME}"
                echo "build num:${BUILD_NUMBER}"
                echo "build stage:${STAGE_NAME}"
                
                '''
            }
                script {
                	sh "touch a.txt"
              		cleanWs()  
          		}
                // sh "git clone abc.git"
                // sh "sleep 3"
                echo "git pull"
                sh 'echo "Hello,\nWorld!"'
                sh 'echo \'Hello,\nWorld!\''
                sh "echo  'Hello,\nWorld!'"      
                sh "echo  \"Hello,\nWorld!\""    
                sh """echo  'Hello 
                  
                  World!' """
                sh 'echo "Hello,\nWorld!"'
                // timeout(time:3,unit:"SECONDS") {
                //     sh "sleep 30"
                // }
            }
             post { 
        always { 
            echo 'always local'
        }
        success { 
            echo 'success local'
        }
        failure { 
            echo 'failure local'
        }
        aborted { 
            echo 'aborted local'
        }
        unstable { 
            echo 'unstable local'
        }        
    }
        }
        stage("test creditionals"){
            
            steps {
               sh 'echo $SERVICE_CREDS'
                 sh 'echo "SSH user is $SSH_CREDS_USR"'
                sh 'echo "SSH passphrase is $SSH_CREDS_PSW"'
            }
        }
        stage("build code") {
            steps{
                 script {
                      env.name3 = "peter"                 
                      env.name4 = "lisha"
                }
                echo "my name is ${env.name3}"
                sh 'echo "my name is ${name4}"'
                echo "build clone"
                print name4
            }
        }
        stage("deploy code") {
            steps{
                echo "deploy clone"
            }
        }
        stage("test code") {
            steps{
                echo "automation test"
            }
        }
        stage("echo environment") {
             environment{
        name="json"
    }
            steps {
                withEnv(['name1=join','name2=jack']){ 
                	echo "my name is ${env.name1}"
                	sh 'echo "my name is ${name2}"'
                }
                sh "echo $CC $name"}
               
               
            
        }
        stage("echo environment common") {
             environment{
        name="json"
    }
            steps {sh "echo $CC"}
            
        }
        stage('parallel test'){
            parallel{
                stage('parallerl-1'){
                    
                    steps{
                        sh "echo 'parallerl-1'"
                        
                    }
                }
                stage('parallerl-2'){
                    
                    steps{
                        sh "echo 'parallerl-2'"
                        
                    }
                }
            }
        }
    }
    
    post { 
        always { 
            echo 'always'
        }
        success { 
            echo 'success'
            script{
                currentBuild.description = "部署成功"
                currentBuild.displayName = "Build#123"
                  manager.addShortText("构建用户：Gary")
            }
            
        }
        failure { 
            echo 'failure'
            script{
                 currentBuild.description = "部署成功"
                currentBuild.displayName = "Build#123"
            }
            
        }
        aborted { 
            echo 'aborted'
        }
        unstable { 
            echo 'unstable'
        }        
    }
}
