def JENKINS_PLTF_GIT_BRANCH = env.BRANCH_NAME

pipeline {
    agent {
        node {
            label 'ubuntu18'
        }
    }
    options { skipDefaultCheckout() }
    parameters {
        choice(name: 'OPERATION_TYPE', choices: " \nUpgrade\nNewInstall", description: 'The type of operation being performed. Please refer to documentation for details of the differences.')
        choice(name: 'PRODUCT_NAME', choices: "advance\nadvise\nrecruit", description: 'Deploy for product name')
        string(name: 'RELEASE_NAME', description: 'The Product release version to install/upgrade')
        string(name: 'SUB_PRODUCT', description: '***Internal Use only***')
        string(name: 'TARGET_POD', description: '')
        extendedChoice(name: 'CUSTOM_ORG_OPERATIONS', type: 'PT_MULTI_SELECT', value:'One,Two,Three,Four,Five,Six,Seven,Eight,Nine,Ten')
        text(name: 'UserInput', description: """<h5>A comma (,) seperated text file (any file name with extension .txt or .csv) listing the configurations.<br></h5>
            Example:<br>
            <table>
            <tr style="border: 1px solid black;">
                <td>Create (New Install)</td>
                <td>Update (Existing Install)</td>    
            </tr>
            <tr>
                <td style="border: 1px solid black;">
                <span>Target,AgOverride,SQLClusterOverride,Locale</span><br>
                value,value,value,lcid_locale_code<br>      
                </td>
                <td style="border: 1px solid black;">
                <span>Target</span><br>
                value<br>
                </td>    
            </tr>
            </table>
            <span style="color:red"><b>Please refer to documentation for information and exmaple on how to setup this file.</b><span>
            <hr>""")
        booleanParam(name: 'DRY_RUN', defaultValue: false, description: """If true, no org operations will run, but the organization json config will be generated. (Pod operations will run)
            <hr><b>If any of the custom operations are selected, they will override any decision to do auto-piecemeal or a full-install.</b>""") 
        booleanParam(name: 'FULL_INSTALL', defaultValue: false, description: """<b>Org operation</b>
            <br>Flag indicating whether to reset piecemeal, and do a full installation.""")        
        booleanParam(name: 'USE_AUTO_PIECEMEAL', defaultValue: false, description: 'Flag indicating whether automatic piecemeal should be used in run. Subsequent runs will resume from last piecemeal step')
        string(name: 'MAX_THREADS', defaultValue: '5', description: '<b>UPGRADES ONLY.</b> - The maximum number of concurrent upgrades processing at one time.')
        booleanParam(name: 'DELETE_EXISTING_ORG', defaultValue: false, description: '<span style="color:red"><b>Set to true ONLY when you want to replace an existing org during NewInstall.</b><span>') 
        string(name: 'EMAIL_LIST', defaultValue: 'nithin.kumar@ellucian.com', description: 'The target email group to get status reports on this install.')
        booleanParam(name: 'CLEAN_WORKSPACE', defaultValue: false, description: """Clean Jenkins Workspace<br>
            Note: Use this option only when other jobs are not running""")
        string(name: 'ADMIN_SERVER_INSTANCE_ID', defaultValue: 'i-0ffea3d6131a4efc4', description: """EU: i-01029f4987d77a499<br>AU: i-04df1e6c0568282ac<br>CCA: i-00dcf8dcd858731de<br>UVA<br>
            <ul><li>epCRMAuva001: i-0ae8af4d7a2ab2e48</li>
            <li>epCRMAuva002: i-03b4b26a5616ebe42</li>
            <li>epCRMAuva003: i-0a3b65ac5c1170a84</li>
            <li>epCRMAuva004: i-0e4ba30a8fd84574b</li></ul>
            <br>dev adfs server: i-0ffea3d6131a4efc4 
            <br>partner adfs server: i-065c184fd11301df0""")
        string(name: 'PLATFORM_PROPERTIES_BRANCH', defaultValue: 'master', description: 'DEV ONLY - override branch details')
        string(name: 'JENKINS_PLTF_GIT_BRANCH', defaultValue: 'develop-pipeline-as-code', description: 'Platform branch name')
    }
    
    stages {
        stage('Pre-Build steps') {
            steps {
                echo "Checkout Platform branch"                                
            }
        }

        stage('Post-Build steps') {
            steps {
                echo "Clean Build Dir: '${PRODUCT_NAME}-${TARGET_POD}-${BUILD_NUMBER}'"
                dir("${PRODUCT_NAME}-${TARGET_POD}-${BUILD_NUMBER}") {
                    deleteDir()
                }
                dir (WORKSPACE) {
                    script{
                        if (CLEAN_WORKSPACE == "true") {
                            echo "Cleaning Jenkins Workspace'"
                            deleteDir()
                        }
                    }
                }                 
            }
        }              
    }
}
