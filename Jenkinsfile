pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {
               sh   'mvn clean package'
            }

            post{
                success{
                    echo    'Now Archiving .... '

                    archiveArtifacts artifacts : '**/*.war'
                }

            }
        }

        stage ('Deploy Build in Staging Area'){
            steps{
                build job : 'Deploy-StagingArea-Piple'
            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout (time: 5, unit:'DAYS'){
                    input message: 'Approve PRODUCTION Deployment?'
                }

                build job : 'Deploy-Production-Pipeline'
            }

            post{
                success{
                    echo 'Deployment on PRODUCTION is Sucessful'
                }

                failure{
                    echo 'Deployment Failure on PRODUCTION'
                }
            }

        }

    }


}
