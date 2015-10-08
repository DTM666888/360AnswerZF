# 360AnswerZF
运维开发软件工程师笔试题
1.	password_cache:
可以设置免密码登录解决问题。
首先在在所有服务器上面按照ssh，设置免密码登录，生成私钥与公钥，然后把公钥追加到authorized_keys中。然后在主服务器上，把公钥发给每个子服务器，然后登录到每个子服务器中，把接受的公钥追加到authorized_keys中。然后就可以在主服务器中免密码登录所有的服务器。
密码放 ssh-keygen -t rsa -P ''” 生成的.ssh文件夹中。

4.log_cutting：
#!/bin/bash
#设置日志文件存放目录
logs_path="/usr/local/nginx/logs/"
#设置pid文件
pid_path="/usr/local/nginx/nginx.pid"
#重命名日志文件
mv ${logs_path}access.log ${logs_path}access_$(date-d"yesterday"+"%Y%m%d").log
#向nginx主进程发信号重新打开日志
kill -USR1 `cat ${pid_path}`
再用crontab –e 每天执行即可。
切割时间不能很好的控制

9.group：
#include <iostream>
#include <vector>
using namespace std;
class Tree
{
public:
	Tree(int k=0):key(k){}
	
	static void Add(Tree * p,Tree* s)
	{
		p->son.push_back(s);
	}
	static void Get(Tree *p)
	{
		vector<Tree* >::iterator ite=p->son.begin();
		for (;ite!=p->son.end();++ite)
		{
			cout<<(*ite)->key<<",";//子节点遍历
		}
	}
private:
	vector<Tree* > son;
	int key;
};

11.vssh：
登录后所有操作相当于同时对n台服务器生效。
对每一个命令都遍历IP主机，分别执行命令
