pipeline {
    agent any

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
                # Create application directory
                sudo mkdir -p /var/www/app

                # Copy the generated JAR to the app directory
                sudo cp target/*.jar /var/www/app/app.jar

                # Stop old running instance (if exists)
                pkill -f app.jar || true

                # Start new application
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
