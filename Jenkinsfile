void setBuildStatus(String message, String state) {
    step([
        $class: "GitHubCommitStatusSetter",
        commitShaSource: [$class: "BuildDataRevisionShaSource"],
        contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "contextSource"],
        errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
        reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/grmmvv/jenkins"],
        statusBackrefSource: [$class: "ManuallyEnteredBackrefSource", backref: "https://www.jenkins.io/doc/pipeline/steps/github"],
        statusResultSource: [
            $class: "ConditionalStatusResultSource",
            results: [[
                $class: "AnyBuildResult", message: message, state: state
            ]]
        ]
    ]);
}

pipeline{
    agent{
        label "ubuntu"
    }
    stages{
        stage("A"){
            steps{
                echo "========executing A========"
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
            setBuildStatus("Complete", "SUCCESS")
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
