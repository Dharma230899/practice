pipeline{
    agent any
    stages{
        stage('build'){
            steps{
                sh '''
                mkdir -p build
                touch build/com.txt
                echo "extra extra small subnet">> build/com.txt
                cat build/com.txt
                '''
            }
        }
        stage('test'){
            steps{
                sh 'test -f build/com.txt'
            }
        }
        stage('QA deploy'){
            steps{
                sh '''
                    WAR_FILE = target/com.war
                    TOMCAT_USER = deployuser
                    TOMCAT_HOSTNAME = qa-server.example.com
                    TOMCAT_WEBAPPS = /tomcat/webapps
                    scp $WAR_FILE $TOMCAT_USER@$TOMCAT_HOSTNAME:$TOMCAT_WEBAPPS
                    ssh $TOMCAT_USER@$TOMCAT_HOSTNAME "systemctl tomcat restart"
                '''
            }

        }
    }
}
