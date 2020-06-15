def JENKINS_PLTF_GIT_BRANCH = env.BRANCH_NAME

pipeline {
    agent {
        node {
            label 'deploy_ubuntu18_prod1'
        }
    }
    options { skipDefaultCheckout() }
    parameters {
        choice(name: 'PRODUCT_NAME', description: 'Deploy for product name', choices: "advance\nadvise\nrecruit")
        string(name: 'RELEASE_NAME', defaultValue: '3.1', description: 'The release you are migrating to')
        string(name: 'SOURCE_POD', defaultValue: 'E-D-CRM-UVA-31', description: 'The source pod name. Format example: E-D-REC-UVA-01')
        string(name: 'TARGET_POD', defaultValue: 'E-D-CRM-UVA-35', description: 'The target pod name. Format example: E-D-REC-UVA-02')
        string(name: 'SETTINGS_POD', description: 'The optional settings pod name, Only useful in a ProdToTest operation type')
        choice(name: 'OPERATION_TYPE', description: 'Deploy for product name', choices: "ProdToProd\nProdToTest")
        booleanParam(name: 'FULL_MIGRATION', defaultValue: false, description: 'Flag indicating whether to reset piecemeal and run all the migration operations')
        booleanParam(name: 'COPY_ARTIFACTS', defaultValue: true, description: '	If true, the pipeline will copy the latest artifacts and scripts to the servers')
        string(name: 'MAX_THREADS', defaultValue: '10', description: 'Maximum number of parallel threads allowable in each powershell runspace.')
        text(name: 'UserInput', description: """<h5>A comma (,) seperated parameter listing the migration configurations.<br></h5> Example:<br> 
            <b>SourceOrg,TargetOrg,SettingsOrg,HulkServer,AgOverride,SQLClusterOverride</b><br> 
            value,value,value,value,value,value<br> 
            <span style="color:green">The Setting Org is optional and if present the job will grab the config and api settings from the given org.<br> </b><span> <hr>
            <h3>CUSTOM_MIGRATION_OPERATIONS<br></h3>""")
        booleanParam(name: 'Hulk_Pre_Import_Source_Steps')
        booleanParam(name: 'Hulk_Pre_Import_Target_Steps')
        booleanParam(name: 'Hulk_Import_Steps')
        booleanParam(name: 'Hulk_Post_Import_Source_Steps')
        booleanParam(name: 'Hulk_Post_Import_Target_Steps')
        booleanParam(name: 'Hulk_Install_Steps')
        booleanParam(name: 'Hulk_Post_Install_Steps')
        booleanParam(name: 'Target_Pre_Import_Source_Steps')
        booleanParam(name: 'Target_Pre_Import_Target_Steps')
        booleanParam(name: 'Target_Import_Steps')
        booleanParam(name: 'Target_Post_Import_Source_Steps')
        booleanParam(name: 'Target_Post_Import_Target_Steps')
        booleanParam(name: 'Target_Install_Steps')
        booleanParam(name: 'Target_Post_Install_Steps')
        booleanParam(name: 'Hulk_Cleanup_Steps')
        
    }
    
    stages {          
        stage('Pre-build steps') {
            steps {
                echo "Pre-build steps'"
                }     
            }
        } 
        stage('Post-build steps') {
            steps {
                echo "Post-build steps'"
                }              
            }
        }         
    }
}
