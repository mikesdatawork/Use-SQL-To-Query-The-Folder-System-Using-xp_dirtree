![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Use SQL To Query The Folder System Using xp_dirtree
**Post Date: December 15, 2014**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's a short piece of SQL Logic that will give you a list of folders, or files from any directory. All you need is access rights to those folders either from the SQL Service account or your regular use account MyDomain\MyUserName.</p>      


## SQL-Logic
```SQL
use master;
set nocount on
 
if object_id('tempdb..#folderandfileinfo') is not null
drop table #folderandfileinfo
 
create table #folderandfileinfo
(
cid int identity(1,1) primary key clustered
,   subdirectory    varchar(255)
,   depth int
,   isfile int
)
 
declare @path   varchar(255)
set @path   = '\\MyBackupShare\MyFolderName' -- insert your path here.
 
insert into #folderandfileinfo
(
[subdirectory]
,   [depth]
,   [isfile]
)
exec master..xp_dirtree
@path
,   1
,   1
 
select
subdirectory
,   depth
,   'object' = case isFile when '1' then 'File' when '0' then 'Folder' end from
#folderandfileinfo
where
subdirectory like '%.bak'
```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

  
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

