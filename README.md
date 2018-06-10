#使用命令创建github代码仓库，push本地仓库到github远程代码仓库

1.利用命令创建github远程代码仓库

　　在将本地代码push到github远程代码仓库之前，总是需要新建github代码仓库，在将本地仓库关联到github远程仓库。其中最为繁琐的操作是建立github代码仓库，需要进入github的网站进行操作，不能借助命令来简化操作，十分繁琐。

　　借助github提供的api，在.bashrc或者.zshrc文件中定义函数，可以利用命令在github上创建代码仓库，十分便捷。

　　首先需要进入github，申请并获取自己的api token，用于鉴权，[地址](https://github.com/settings/tokens/new)在这。

　　 然后在本机使用的bash的配置文件中加入下述函数定义：

复制代码

```
github-create() 
{if [ $1 ]
then
    repo_name=$1
else
    repo_name=`basename $(pwd)`
    echo "set Repo name to ${repo_name}"
fi 
curl -u 'username:api_token' https://api.github.com/user/repos -d '{"name":"'$repo_name'"}'
git remote add origin git@github.com:username/$repo_name.git
}
```

　　注意，需要使用自己的username与api_token覆盖上述函数中相应的值。

　　如果需要在github上创建代码仓库，只需输入命令：

```
　　　　github-create repo_name
```

　　会完成在github上创建名为repo_name的代码仓库的操作。如果没有指定repo_name，会自动将当前路径的文件夹名称设置为代码仓库的名称。

2.将本地代码仓库push到github远程代码仓库

　以下省去在本地创建git仓库以及提交commit等操作。

　(1)首先将本地仓库和远程代码仓库进行关联：
```
　git remote add origin your_repo_url.git
```
　(2)然后将本地代码仓库push到github：
```
　git push -u origin master
```

-------------------------
# hello-world
just another repository


Hi World!

Hubot here, I like Node.js and Coffeescript.
I've had tacos on the moon and find them far superior to Earth tacos.
