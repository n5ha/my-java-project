pipeline{
    agent{
        label "node1"
    }
    tools{
        maven "maven123"
    }
    options{
        skipDefaultCheckout(true)
    }
    stages{
        stage("clone"){
            steps{
            checkout scm
            } 
        }
        stage("build"){
            steps{
                echo "build stage"
                sh"mvn clean package"
            }
        }
        stage("deploy"){
            steps{
                echo "deploy stage"
                sh"""
                    cp  /home/student/jenkinsdirectory/workspace/github_pipeline/target/*.war /usr/share/tomcat/webapps/
                """
                dir("/usr/share/tomcat/webapps/"){
                    sh"""
                    jar -xvf *.war
                    cp -r /usr/share/tomcat/webapps/java-tomcat-maven-example/*  ROOT/
                    """
                }
            }
        }
        stage("cleanup"){
            steps{
                sh"rm -rf /usr/share/tomcat/webapps/java-tomcat-maven-example*"
            }
        }
    }
}