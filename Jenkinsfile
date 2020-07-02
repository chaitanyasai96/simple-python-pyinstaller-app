    pipeline{
        agent none
        stages{
         stage('Build'){
                agent{
                    docker{
                        image 'python:3-slim'
                    }
                steps{
                    sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                    stash(name:'compiled-files', includes:'sources/*.py*')
                }
                }
            }
         stage('Test'){
            agent{
                docker{
                    image 'qnip/pytest'
                }
            steps{
                sh 'py.test --juint-xml test-reports/results.xml sources/test_calc.py'
            }
            post{
                always{
                       junit 'test-reports/results.xml'
                }
            }
    
         }
        }
        }
    }
