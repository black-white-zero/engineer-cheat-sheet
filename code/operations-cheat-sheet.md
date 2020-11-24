# operations-cheat-sheet

> 整理记录自己常用的运维操作指令。
  - [Linux 操作指令](#linux-操作指令)
    - [进程](#进程)
    - [服务](#服务)
    - [文件](#文件)
    - [性能](#性能)
  - [vim 操作指令](#vim-操作指令)
  - [tmux 操作指令](#tmux-操作指令)
  - [python3 操作指令](#python3-操作指令)
  - [django 操作指令](#django-操作指令)
  - [iterm2 操作指令](#iterm2-操作指令)
  - [mysql 操作指令](#mysql-操作指令)
  - [nginx 操作指令](#nginx-操作指令)
  - [git 操作指令](#git-操作指令)
  - [docker 操作指令](#docker-操作指令)

## Linux 操作指令

### 进程
指令 | 用法 | 示例
---------|----------|---------
`lsof -i:[端口号]` | 根据端口号列出进程调用情况 | 查看端口号 8000 的进程调用情况：`lsof -i:8000`
`kill -HUP [进程 ID 号]` | 重启进程 | 重启进程 ID 号为 43389 的进程：`kill -HUP 43389`
`ps -ef \| grep [字符串]` | 根据字符串查找相关的进程 | 查看与 btc 相关进程运行情况：`ps -ef \| grep btc`

### 服务
 指令 | 用法 | 示例
---------|----------|---------
`systemctl start [服务名]` | 启动服务 | 启动 neo4j 服务：`systemctl start neo4j`
`systemctl status [服务名]` | 检查服务状态 | 检查 mysql 的服务状态：`systemctl status mysql.service`
`service [服务名] stop` | 关闭服务 | 关闭 mysql 的服务：`service mysql stop`

### 文件
指令 | 用法 | 示例
---------|----------|---------
`pwd [文件名]` | 获取到文件的绝对路径 | 无
`wc -l [文件名]` | 获取文件行数 | 无
`ls -lht` | 查看当前目录下的文件大小 | 无
`grep -c [字符串] [文件名]` | 查看文件中出现字符串的行数 | 统计日志文件 test.log 中的"ERROR"出现的行数：`grep -c 'ERROR' test.log`
`grep -r --include="*.py" "[字符串]" . -l` | 当前目录及子目录下文件包含字符串的 py 脚本列表 | 无
`tail -f [文件路径]` | 动态查看文件 | 无
`tar -czvf [压缩后文件名].tar.gz [文件名]` | 压缩文件 | 无
`tar -xzvf [压缩后文件名].tar.gz` | 解压文件 | 无
`sha256sum [文件名]` | 数据传输后验证文件完整性 | 无
`sudo vim /etc/hosts` | 更改 hosts 文件 | 无

### 性能
指令 | 用法 | 示例
---------|----------|---------
`df -hl` | 查看磁盘使用空间 | 无
`htop` | 查看资源使用情况 | 无

### 定时任务
指令 | 用法 | 示例
---------|----------|---------
`*/时间 * * * * cd 脚本路径 && venv路径/venv/bin/python3 -u py脚本 >> 日志文件名.log 2>&1` | 定时运行某 py 脚本，并将标准输出和标准错误输出都输出到日志文件 | 无

## vim 操作指令
指令 | 用法 | 示例
---------|----------|---------
`e` | 光标定位到目前单词的末尾 | 无
`b` | 光标定位到目前单词的开始 | 无
`0` | 光标定位到一行的开始 | 无
`$` | 光标定位到一行的末尾 | 无
`G` | 光标定位到末尾一行 | 无
`H` | 光标定位到当前屏幕的第一行 | 无
`M` | 光标定位到当前屏幕的中间行 | 无
`L` | 光标定位到当前屏幕的最后一行 | 无
`:[行号]` | 光标定位到相应的行数 | 无
`dd` | 删除当前行 | 无
`x` | 删除光标后的字母 | 无
`i` | 在光标之前插入字符 | 无
`I` | 在当前行的开始插入字符 | 无
`a` | 在光标之后插入字符 | 无
`A` | 在当前行的结束插入字符 | 无
`o` | 在光标下一行新建一行并插入字符 | 无
`/[正则表达式]` | 回车后光标定位到查询的位置（n N 进行上下翻动） | 无
`u` | 撤销上一次的操作 | 无
`U` | 撤销所有在这一行做的操作 | 无
`ctrl + r` | 重新恢复上一次的操作 | 无
`:%s/[字符串 A]/[字符串 B]/g` | 全局将字符串 A 替换为字符串 B | 无

## tmux 操作指令
指令 | 用法 | 示例
---------|----------|---------
`tmux` | 开始一个新会话 | 无
`tmux ls` | 查看会话列表 | 无
`tmux a -t [会话名]` | 进入到相应名称的会话 | 无
`tmux kill-session -t [会话名]` | 删除相应名称的会话 | 无
`ctrl+b d` | 离开当前会话 | 无
`ctrl+b p` | 切换上一窗口 | 无
`ctrl+b n` | 切换下一窗口 | 无
`ctrl+b c` | 新建窗口 | 无
`ctrl+b &` | 关闭当前窗口 | 无
`ctrl+b %` | 当前面板左右一分为二，右侧新建面板 | 无
`ctrl+b "` | 当前面板上下一分为二，下侧新建面板 | 无
`ctrl+b 左右方向键` | 向左或向右切换面板 | 无
`ctrl+b x` | 删除当前面板 | 无
`ctrl+b [` | 进入翻页模式（可查看面板中上面隐藏的信息）| 无

## python3 操作指令
指令 | 用法 | 示例
---------|----------|---------
`pip3 list \| grep [字符串]` | 查看安装与字符串相关 pip 包的情况 | 查看是否安装 request 库：`pip3 list \| grep request`
`python3 -m venv [虚拟环境文件夹名]` | 创建虚拟环境 | 无
`source [虚拟环境文件夹名]/bin/activate` | 激活虚拟环境 | 无
`deactivate` | 退出虚拟环境 | 无
`pip3 install [pip 包名] -i https://pypi.tuna.tsinghua.edu.cn/simple` | pip3 第三方库安装（镜像） | 无
`pip3 freeze > requirements.txt` | pip3 生成 requirements.txt 依赖包文件 | 无
`pip3 install -r requirements.txt` | pip3 安装 requirements.txt | 无
`python3 -m unittest xxx_test` | 运行单元测试 | 无
`python3 manage.py makemigrations` | 根据 Model 的改动创建新 migrate | 无
`python3 manage.py migrate` | 根据 migrate 文件情况将 Model 改动同步到数据库 | 无

## django 操作指令
指令 | 用法 | 示例
---------|----------|---------
`python3 manage.py collectstatic` | 静态文件生成 | 无
`python3 manage.py runserver [ip]:[端口号]` | 在对应 ip 和端口号运行 django 服务 | `python3 manage.py runserver 127.0.0.1:8000`

## iterm2 操作指令
指令 | 用法 | 示例
---------|----------|---------
`ctrl+w` | 删除光标的前一个单词 | 无
`ctrl+l` | 清除屏幕 | 无
`ctrl+a` | 光标移到行首 | 无
`ctrl+e` | 光标移到行尾 | 无
`option+左右方向键` | 向前向后移动单词 | 无

## mysql 操作指令
指令 | 用法 | 示例
---------|----------|---------
`mysql -h 127.0.0.1 -u [用户名] -p` | docker-mysql 登录指令 | 无
`mysql -u [用户名] -p` | mysql 登录指令 | 无
`create database [数据库名];` | 创建数据库 | 无
`show databases;` | 查看数据库列表 | 无
`use [数据库名];` | 使用数据库 | 无
`show tables;` | 查看数据表列表 | 无
`truncate [数据表名];` | 清空数据表 | 无
`desc [数据表名];` | 查看表结构 | 无
`show create table [数据表名];` | 查看创建表的 DDL 语句 | 无
`select count(*) from [数据表名];` | 查看数据表中记录的条数 | 无
`alter table [数据表名] add [字段名] [字段类型];` | 添加字段 | 无
`alter table [数据表名] drop index [唯一约束字段名];` | 删除字段唯一约束 | 无
`alter table [数据表名] modify [字段名] [字段类型];` | 修改字段类型 | 无
`alter table [数据表名] add unique([唯一约束字段名]);` | 添加字段唯一约束 | 无
`alter table [数据表名] convert to character set utf8mb4;` | 更改字符类型为 utf8mb4 | 无
`create user '[用户名]'@'[主机名]' identified by '[密码]';` | 创建用户 | 无
`grant all privileges on [数据库名].* to '[用户名]'@'[主机名]';` `flush privileges;` | 授权用户拥有某个数据库全部权限 | 无
`grant all privileges on [数据库名].* to '[用户名]'@'[主机名]'; flush privileges;` | 授权用户拥有某个数据库全部权限 | 无
`update [数据表名] set [字段名]=[更改值] where [查询字段名]=[查询字段值];` | 更新数据表字段值 | 无
`INSERT INTO [数据表名] ( [字段名 1], [字段名 2], ... ) VALUES ( [字段值 1], [字段值 2], ... );` | 新增一条数据 | 无
`delete from [数据表名] where [查询字段名]=[查询字段值];` | 删除对应记录 | 无
`create table [备份表名] like [被备份表名];` `insert into [备份表名] select * from [被备份表名];` | 表备份 | 无
`use information_schema;` `select concat(round(sum(data_length/1024/1024),2),'MB') as data from tables where table_schema='[数据库名]' and table_name='[数据表名]';` | 查看数据表存储大小 | 无
`mysqldump -h 127.0.0.1 -u [用户名] -p [数据库名] [数据表名] > [导出数据表路径]/[文件名].sql` | 导出数据表 | 无
`source [文件名]` | 导入数据表 | 无
`select [字段名] from [数据表名] where [where 子句] into outfile '[文件路径]';` | 查询结果导出到文件 | 无

## nginx 操作指令
指令 | 用法 | 示例
---------|----------|---------
`nginx -t -c /etc/nginx/nginx.conf` | 测试 nginx | 无
`vim /etc/nginx/nginx.conf` | 配置 nginx | 无
`cd /etc/nginx/conf.d/` | cd 到 nginx 配置目录 | 无
`service nginx start` | 启动 nginx | 无
`service nginx restart` | 重启 nginx | 无

## git 操作指令
指令 | 用法 | 示例
---------|----------|---------
`git init` | 初始化 git | 无
`git remote add origin [git clone 链接]` | 为初始化的 git 添加远程仓库(后 origin 即为 git clone 链接) | 无
`git checkout -b [分支名]` | 切换分支 | 无
`git checkout [想撤销的文件名]` | 撤销对指定文件的修改(若为.，即所有已修改但未提交的文件，不包括新增的文件) | 无
`git reset HEAD [想撤销的文件名]` | 对添加文件后的撤销 | 无
`cd [代码所在目录]` `git init` `git remote add origin git@github.com:slowmist/[git clone 链接]` `git pull origin master:master` `git status` `git add [添加文件名]` `git commit -m "[提交备注内容]"` `git push -u origin master` | 已有代码 push 到 git | 无

## docker 操作指令
指令 | 用法 | 示例
---------|----------|---------
`docker ps -a` | 查看 docker 中的容器列表 | 无
`docker start [容器 ID]` | 启动对应的容器 | 无

## Neo4j-Cypher 操作指令
指令 | 用法 | 示例
---------|----------|---------
`CREATE INDEX ON :标签名(属性名);` | 添加索引 | 无
`:schema` | 查看索引添加情况 | 无
`MATCH (n:标签名) WHERE n.属性名="属性值" RETURN n;` | 根据标签名和属性值筛选图数据 | 无
`profile MATCH (n:标签名) WHERE n.属性名="属性值" RETURN n;` | 查看图数据筛选执行计划 | 无
