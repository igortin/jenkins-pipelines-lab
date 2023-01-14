pipeline{
    agent any

    parameters {
        booleanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
    }

    stages{
        stage("Test"){
            parallel {
                stage("Unit tests"){
                    steps{
                        sh ' ./mvnw test -D testGroups=unit.'
                    }   
                }
                stage("Integration tests"){
                    steps{
                       sh './mvnw test -D testGroups=integration'
                    }
                    when {
                        expression { return params.RUN_INTEGRATION_TESTS }
                    }
                }
                stage ("Build"){
                    steps {
                        script {
                            try {
                                sh './mvnw package -D skipTests'
                            }
                            catch (ex) {
                                echo "Error while generating JAR file"
                                throw ex
                            }
                        }
                    }
                }
                 stage ("Deploy"){
                    
                    input {
                            message 'Deploy the application?'
                        }                    
                    
                    steps {
                        echo "Deploy..."
                    }
                }
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}