https://notes.wanghao.work/2015-07-06-%E8%87%AA%E5%8A%A8%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6.html

---------------------------backupΪ����Դ�ļ��Զ����ݽű�--------------------------

1.��װ`shelljs`ģ��

$ npm install --save shelljs 

2.��д�Զ����ݽű�

ģ�鰲װ���֮����hexo��Ŀ¼��`scripts`�ļ��У�*û�о��½�*���½�backup.js�ļ���
д��һ�����ݣ�

require('shelljs/global');
try {
	hexo.on('deployAfter', function() {//��deploy��ɺ�ִ�б���
		run();
	});
} catch (e) {
	console.log("������һ������<(��3��)> !����������Ϊ��" + e.toString());
}
function run() {
	if (!which('git')) {
		echo('Sorry, this script requires git');
		exit(1);
	} else {
		echo("======================Auto Backup Begin===========================");
		cd('H:\My_project\myBlog');  //�˴��޸�ΪHexo��Ŀ¼·��
		if (exec('git add --all').code !== 0) {
			echo('Error: Git add failed');
			exit(1);
		}
		if (exec('git commit -am "Form auto backup script\'s commit"').code !== 0) {
			echo('Error: Git commit failed');
			exit(1);
		}
		if (exec('git push origin master').code !== 0) {  //�˴��޸�Ϊ�Լ���Զ�ֿ̲����ͷ�֧��
			echo('Error: Git push failed');
			exit(1);
		}
		echo("==================Auto Backup Complete============================")
	}
}


���У���Ҫ�޸ĵ�17�е�D:/hexo·��ΪHexo�ĸ�Ŀ¼·�������ű��е�·��Ϊ������Hexo·����

cd('D:/hexo');    //�˴��޸�ΪHexo��Ŀ¼·��

������GitԶ�ֿ̲����Ʋ�Ϊorigin�Ļ�������Ҫ�޸ĵ�28��ִ�е�push����޸ĳ��Լ���Զ�ֿ̲�������Ӧ�ķ�֧����

if (exec('git push origin master').code !== 0) {


---------------------------sublimeΪ��������Զ��򿪱༭���ű�---------------------

�������windowsƽ̨��Hexo�û�������������д����Ľű���


var spawn = require('child_process').exec;
// Hexo 2.x �û��������
hexo.on('new', function(path){
  exec('start  "markdown�༭������·��.exe" ' + path);
});
// Hexo 3 �û��������
hexo.on('new', function(data){
  exec('start  "markdown�༭������·��.exe" ' + data.path);
});




�������Macƽ̨Hexo�û�������������д����Ľű���


var exec = require('child_process').exec;
// Hexo 2.x �û��������
hexo.on('new', function(path){
    exec('open -a "markdown�༭������·��.app" ' + path);
});
// Hexo 3 �û��������
hexo.on('new', function(data){
    exec('open -a "markdown�༭������·��.app" ' + data.path);
});