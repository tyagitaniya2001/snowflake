pipeline {
    agent any
    stages {

        stage('Test run') {
            steps {
                echo "Production Deployment with Schemachange"
                }
            }

        stage('Get Schemachange') {
            steps{
                bat "git clone https://github.com/Snowflake-Labs/schemachange.git"
                }
            }

        stage('Run schemachange') {
            steps {
                    withCredentials(bindings: [usernamePassword(credentialsId: 'snow_cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) 
                    {

                        bat "python3 -m pip install schemachange --upgrade"
                        bat "python3 schemachange/schemachange/cli.py deploy -f migrations -a ${SF_ACCOUNT} -u ${USERNAME} -r ${SF_ROLE} -w ${SF_WAREHOUSE} -d ${SF_DATABASE} -c ${SF_DATABASE}.SCHEMACHANGE.CHANGE_HISTORY --create-change-history-table"
                         }  
               }
        }
    }
}