pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Geetha-R-27/car.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                sudo mkdir -p /var/www/app

                sudo cp target/*.jar /var/www/app/app.jar

                pkill -f app.jar || true

                nohup java -jar /var/www/app/app.jar > /var/www/app/log.out 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo "Java Application Deployed Successfully!"
        }
    }
}
