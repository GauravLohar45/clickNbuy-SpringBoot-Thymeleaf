pipeline {
    agent any

     environment {
        JAVA_HOME = "/ACTUAL/JAVA/PATH"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

  tools {
    jdk 'JAVA_HOME'
    maven 'maven'
}

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Stop Old App') {
            steps {
                sh '''
                PID=$(ps -ef | grep java | grep jar | awk '{print $2}')
                if [ ! -z "$PID" ]; then
                  kill -9 $PID
                fi
                '''
            }
        }

        stage('Run App') {
            steps {
                sh '''
                nohup java -jar target/*.jar > app.log 2>&1 &
                '''
            }
        }
    }
}
