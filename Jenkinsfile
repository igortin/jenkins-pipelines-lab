pipeline{
    agent{
        label "any"
    }

   
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