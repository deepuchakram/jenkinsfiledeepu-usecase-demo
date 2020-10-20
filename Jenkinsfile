pipeline {
    agent any 
    environment{
        PATH= "C:/Users/Apache Software Foundation/apache-maven-3.5.2:$PATH"
       
    }
    stages {
        stage('Build') {
            steps {
                // Download the code
                checkout scm
                // Compile the main class
                shell 'javac -d target -sourcepath src/main/java src/main/java/com/example/math/Calculator.java'
            }
        }
        stage('Test') {
            steps {
                // Compile the tests
                shell 'javac -d target -cp target:junit-platform-console-standalone-1.4.0.jar src/test/java/com/example/math/TestCalculator.java'
                // Run the tests
                shell 'java -jar junit-platform-console-standalone-1.4.0.jar --class-path target --scan-class-path --reports-dir=target/surefire-reports/'
            }
        }
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'maven-3.5.2') {
                    shell 'mvn deploy'
                }
            }
        }
    }
}
    

