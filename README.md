初识分布式是代码管理工具
 
  默认操作步骤
   1. mkdir 目录 新建文件 
   2. git add xx.txt (放入暂存区)
   3. git commit -m 'first commit' (本地仓库初初始化)
   4. git reomte add orgin ssh地址 (本地仓库与远程仓库建立关联)
   5. git push -u origin master (第一次提交本地仓库master 分支到远程仓库)


  一直会报以下问题：
   error Permission to richChen0815/gittest.git denied to 13526557907.
   fatal: Could not read from remote repository.
   
   大致意思:许可证书被拒绝了 无法从远程库读取  Permission 证书 denied 拒绝  fatal 致命
	 
   这个问题让我想到了是不是ssh 配置有问题。
   
   以下是ssh 配置过程
   
	  1. ssh-keygen -t rsa -C 'richeChen0815' -f 'testkey'
	   
	  2.github add ssh-key 
	   
		网上说 -C 需要写成github 的登陆的用户名,这里也试着做了。
	 
	  3.ssh -T git@github.com
	   
	   提示 You've successfully authenticated, but GitHub does not provide shell access.
	   
	   貌似有戏，然后再次push origin , 但是还是会报相同的错误，又被拒绝的，无法读取。
	   
	   
	   
	   
	  ssh -v git@github.com
	  
	  报了一大推debug
	  
	  ssh-agent -s 
		SSH_AUTH_SOCK=/tmp/ssh-ajmsxTBFl1Mt/agent.787; export SSH_AUTH_SOCK;
		SSH_AGENT_PID=788; export SSH_AGENT_PID;
		echo Agent pid 788;

	  ssh-agent bash  开启ssh-agent

	  ssh-add ~/.ssh/testkey 添加私钥
	  
	   Could not open a connection to your authentication agent.
	   
	   需要先执行 ssh-agent bash,然后再执行 ssh ~/.ssh/testkey

	  
	   提示添加标识了，反正不一样的的提示。。哈哈，有戏
	   Identity added: /c/Users/Administrator/.ssh/testkey (richChen0815)
	
	
	在执行远程提交操作成功了。。。
		
		
		
	总结：ssh-add 是把密钥放到ssh-agent 缓存中。问题出在ssh 私密钥没有读取。我的系统是windows ,我是在桌面生成一个密钥对，然后复制到用户名下的.ssh目录。只能在一个窗口中使用。其他窗口如果没有配置就不生效。
	
	
	  



git 常用命令
   本地操作
      1.添加文件
        git add .  

      2.提交到本地仓库
        git commit -m 'xxx'

      3.查看工作区文件修改状态
        git status

      4.查看日志
        git log  /   git reflog

      5.版本切换
       git reset --hard [coomit id | HEAD^^^^^^]
       
    本地仓库与远程
      1.  git clone ssh 克隆远程仓库 
              
      2.git pull origin master
     
      3.git push orgin master (如果远程没有master分支，会自动创建master分支)
      
      4.git remote add origin xxx 本地关联远程仓库  默认是maste分支
      
   
   分支管理
   
      1.git branch xx
      
      2.git checkout xx
      
      简写成 git checkout -b xx  切换并创建分支
      
      3.git branch -d xx  删除分支
      
      4.git merge dev   先切换到你要的分支，然后执行该操作。大致的意思就是 你把dev 分支过来。 接着你可以把不需要的分支remove.

      5. git checkout -b dev origin/dev 创建与远程对应分支
     
      
      工作区          缓存区           本地仓库      远程仓库 区别
   
      工作区间       git add (stage)  git init       github
   
   
   合并远程分支操作
   
   本地分支merge 后，在推动到远程分支。本地合并完成在提交。
   
   
   初始化工作区间设置以及提交的用户名邮箱信息
      git init
      git config --global user.name ''
      git config --global user.email ''
   
   
   
   
   
  
   
   
   
     
     
    
     
   
	
	
	   
	 
	
   
   
   
   
   

