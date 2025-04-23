pipeline{
    agent any
    tools{
        maven "Maven"
        jdk "Java"
    }
    environment{
        JAVA_HOME = tool "Java"
    }
    stages{
        stage('initialize'){
            steps{
                bat 'echo pipeline started'
            }
        }
        stage('checkout'){
            steps{
                git url:'https://github.com/spring-projects/spring-petclinic.git',
                branch:'main'
            }
        }
        stage('build'){
              steps{
                  bat '.\\mvnw.cmd clean package'
              }
        }
        stage('test'){
            steps{
                bat '.\\mvnw.cmd test'
            }
            //exporting text result
            post{
                always{
                    junit 'target\\surefire-reports\\*.xml'
                }
            }
        }

        stage('run'){
            steps{
                bat '''for %%f in (target\\*.jar) do "%JAVA_HOME%\\bin\\java" -Dserver.port=8090 -jar "%%f"'''
            }
        }
    }
}
