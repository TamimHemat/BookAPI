/*  Tamim Hemat  (A01278451)

    Date: April 11-th, 2023

    Description: This is a pipeline for a Python project that will have the following stages:
    - Build: Install all the dependencies and print some specific output to the console
    - Code Quality: Run the linter (pylint-fail-under) on all Python files and fail the pipeline if the score is below 7.0
    - Code Quantity: Run a command that will output the number of Python files
    - Test: Run the unit tests only if the boolean parameter called TEST is set to true and post the results.
    - Package: Create a zip file called package.zip containing all the Python files in the project.
               The zip file should be created made into a build artifact so it can be downloaded from Jenkins.
    
    The pipeline should have the following parameters:
    - TEST: A boolean parameter that will be used to determine if the tests should be run or not. Defaults to false.
*/ 


pipeline{
    agent any
    parameters{
        booleanParam(defaultValue: false, description: 'Run the tests?', name: 'TEST')
    }
    stages{
        stage('Build'){
            steps{
                sh 'echo "Installing the Python Requirements..."'
                sh 'pip install -r requirements.txt'
                sh 'echo "Requirements complete."'
            }
        }
        stage('Code Quality'){
            steps{
                sh 'pylint-fail-under --fail_under 7.0 *.py'
            }
        }
        stage('Code Quantity'){
            steps{
                sh 'echo "Number of Python files: $(ls | grep -E "*.py$" | wc -l)"'
                sh 'echo "My student number: A01278451 (Tamim Hemat)"'
                sh 'echo "My group number: 3"'
            }
        }
        stage('Test'){
            when{
                expression{params.TEST}
            }
            steps{
                sh 'python3 test_book_manager.py'
            }
            post{
                always{
                    junit 'test-reports/*.xml'
                }
            }
        }
        stage('Package'){
            steps{
                sh 'zip package.zip *.py'
                archiveArtifacts artifacts: 'package.zip'
            }
        }
    }
}