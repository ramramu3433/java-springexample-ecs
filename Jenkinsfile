pipeline {
    agent any
    
    stages {
         stage('checkout')
             {
                 steps
                 {
                 checkout scm
                 }
}
       stage('build')
       {
           steps
           {
              sh('mvn clean install')
           }
       }
       stage('deploy')
       {
steps{
      script {
                        file= sh "ls /home/janakiraman/apache/webapps/ | grep app1.war"
                        if (env.file=="app1.war")
                        sh 'cp /home/janakiraman/apache/webapps/app1*.war /home/janakiraman/backups/app1.war'
      }
      sh 'cp target/*.war /home/janakiraman/apache/webapps/.' 
      file= sh 'ls /home/janakiraman/apache/webapps/ | grep app1*.war' | cut -d . -f 1'
}

       }
   stage('test_deploy')
   {
       steps{
           sh 'result=curl -s -o /dev/null -w %{http_code} localhost:8081/$file'
           script{
                       if (env.result==200)
                       {
                           echo 'deployment successful'
                       }
                       else
                       {
                           echo 'deployment failure'
                           exit -1
                       }
           }

       }
   }
    }
}    