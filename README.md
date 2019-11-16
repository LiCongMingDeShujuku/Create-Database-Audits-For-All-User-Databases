![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 为所有用户数据库创建数据库审计
#### Create Database Audits For All User Databases
**发布-日期: 2014年07月10日 (评论)**

![#](images/image0012.png?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
你的SQL审计设置很酷，但现在要捕获所有的SELECT，INSERT，UPDATE，DELETES，EXECUTES等。
（顺便说一下，如果你对SQL Auditing不熟悉，ApexSQL有一篇很好的相关帖子：http：//solutioncenter.apexsql.com/sql-server-database-auditing-techniques/）
你可以用此小脚本在所有数据库中创建统一的审计捕获。如果你要查看每个单独的审计配置，需要做的就是将最后一行更改为：`select（@create_db_audits）for xml path（“），type`。

## English
So you have your SQL Audit setup which is cool, but now you want to capture all the SELECT, INSERT, UPDATE, DELETES, EXECUTES, etc..
( By the way if you’re somewhat new at SQL Auditing ApexSQL has an excellent post about it here: http://solutioncenter.apexsql.com/sql-server-database-auditing-techniques/ )
You can use this little script to create a uniform audit capture across all the databases. If you want to see each individual audit configuration; all you need to do is change the last line to this: `select (@create_db_audits) for xml path(”), type`


---
## Logic
```SQL
use master;
set nocount on
 
declare	@create_db_audits varchar(max)
set 	@create_db_audits = ''
select 	@create_db_audits = @create_db_audits + 'use [' + name + '];' + char(10) +
'create database audit specification [UserAccessAudit_' + name + ']' + char(10) + 'for server audit [MyServerAuditName]' + char(10) +
'add (select, insert, update, delete, execute, receive, references on database::' + name + ' by public)' + char(10) + 'with (state = on);' + char(10) + char(10)
from 
	sys.databases 
where 
	name not in ('master', 'model', 'msdb', 'tempdb')
 
exec (@create_db_audits) --for xml path(''), type


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

