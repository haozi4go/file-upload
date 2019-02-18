pipeline {
  agent any
  environment { 
    update_project_type = 'jar' //war zip jar
  }
  parameters{
    choice(name: 'upload_host', choices: '140.143.246.85:test\n140.143.246.85:prod\n', description: '请选择上传的目标主机')
    string(name: 'upload_dir', defaultValue: '/root/upload', description: '请选择上传的目录')
    string(name: 'upload_file', defaultValue: '/root/upload', description: '请选择上传的文件')
  }
  stages {
    stage('uploading') {
      options {
        timeout(time: 2, unit: 'MINUTES') 
      }
      steps {
        sh "scp ${upload_file} root@\$(echo ${update_host} | cut -d \":\" -f1)  "  // 检测到指定内容started则退出
        echo "Restart success."
      }
    }
    stage('Check') {
      steps {
        sh "ssh root@\$(echo ${update_host} | cut -d \":\" -f1) 'ps -ef|grep ${update_project} | grep -v grep' "
        echo "Check running success."
      }
    }

  }
}
