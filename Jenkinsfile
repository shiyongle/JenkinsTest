pipeline {
   agent {
       label "${params.test_PC}"
   }
   triggers {
        cron('H * * * *')
   }
   parameters {
        gitParameter(name: 'branch', branch: '', branchFilter: '.*', defaultValue: 'origin/master', description: '代码分支', quickFilterEnabled: false, selectedValue: 'NONE', sortMode: 'NONE', tagFilter: '*', type: 'PT_BRANCH')
        choice(name: 'test_PC', choices: ['a', 'b'], description: '执行设备')
        choice(name: 'headless', choices: ['false', 'true'], description: '是否不显示浏览器界面')
        choice(name: 'concurrent', choices: ['否', '1', '2', '3', '4', 'auto'], description: '是否并发执行,并发数')
        string(name: 'robot', defaultValue: '', description: '企业微信群机器人地址,以逗号分隔')
        string(name: 'email', defaultValue: '', description: '邮箱地址,以逗号分隔')
        text(name: 'cases', defaultValue: '''''', description: '要执行的用例', )
   }
   stages {
      stage('克隆代码'){
          steps{
              checkout([$class: 'GitSCM', branches: [[name: "${params.branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], gitTool: 'Default', submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/shiyongle/JenkinsTest.git',credentialsId: 'shiyl',]]])
          }
      }
      stage('执行测试'){
         steps{
             dir("${env.WORKSPACE}/src/cases_ui/") {
             sh ""
                    sh '''
                    python3 allure_debug.py
                    exit 0
                    '''
                        }
                }
      }
      stage('生成Allure报告'){
        steps{
            allure includeProperties: false, jdk: '', results: [[path: 'report/allure_results']]
        }
      }
   }
}
