# README

---

`字典来自网络,仅供学习和研究使用,请勿将字典用于非法用途,任何人造成的任何负面影响,与本人无关.`

---

# 分类

```
端口字典
    按照端口渗透的想法,将不同端口承载的服务可爆破点作为字典内容

Web 字典
    顾名思义,在 web 渗透过程中出现的可爆破点作为字典内容

杂项字典
    目前是按排除法,除 web 和端口外的全部归类为杂项字典
```

---

# 来源
- [boy-hack/wooyun-payload](https://github.com/boy-hack/wooyun-payload)
- [Stardustsky/SaiDict](https://github.com/Stardustsky/SaiDict)
- [rootphantomer/Blasting_dictionary](https://github.com/rootphantomer/Blasting_dictionary)
- [Weakpass](https://weakpass.com/)
- [danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)
- [r35tart/RW_Password](https://github.com/r35tart/RW_Password)
- [wainshine/Chinese-Names-Corpus](https://github.com/wainshine/Chinese-Names-Corpus)
- [modood/Administrative-divisions-of-China](https://github.com/modood/Administrative-divisions-of-China)
- [berzerk0/Probable-Wordlists](https://github.com/berzerk0/Probable-Wordlists)
- [H4lo/dictionary](https://github.com/H4lo/dictionary)
- [TheKingOfDuck/fuzzDicts](https://github.com/TheKingOfDuck/fuzzDicts)
- [Bo0oM/fuzz.txt](https://github.com/Bo0oM/fuzz.txt)
- [EdOverflow/bugbounty-cheatsheet](https://github.com/EdOverflow/bugbounty-cheatsheet)
- [tennc/fuzzdb](https://github.com/tennc/fuzzdb)
- [7dog7/bottleneckOsmosis](https://github.com/7dog7/bottleneckOsmosis)
- [k8gege/PasswordDic](https://github.com/k8gege/PasswordDic)

---

# 特点
1. 整合以上来源 80% 以上内容
2. 任意字典使用数据库去重
3. 删掉一些离谱的比如 "dfasddsf"、"20100112"

---

# 常用的数据库语句

**SQL 查询重复出现次数最多的记录,按出现频率排序**
```sql
SELECT keyword, count( * ) AS count
FROM article_keyword
GROUP BY keyword
ORDER BY count DESC
LIMIT 20
```

**查询不重复的记录**
```sql
select distinct * from tableName
```

**查询不重复的记录转入其他表**

- 新表
    ```sql
    create table tab2 as select distinct * from tab1
    ```

- 存在的表
    ```sql
    insert into tab2 select distinct * from tab1
    ```

**查询A表有但B表没有**
```sql
select a.name
from tab1 a left join tab2 b
on a.name = b.name
where b.name is null
```

**不应该出现在web目录字典的字符**
```
!
@
#
$
%
^
&
*
(
)
--
=
>
<
;
:
"
'
,
?
½
|
{
}
+
//
/_
_/
__
_.
/\
2001
2002
2003
2004
2005
2006
2007
2008
2009
2010
2011
2012
2013
2014
2015
2016
空格
/1/
/2/
/3/
/4/
/5/
/6/
/7/
/8/
/9/
¿
±
¼
°
÷
»
..
./
\
```

**直接查询上述**
```
SELECT * FROM `tab1` where text like '%\!%'
or text like '%\@%'
or text like '%\#%'
or text like '%\$%'
or text like '%\%%'
or text like '%\^%'
or text like '%\&%'
or text like '%\*%'
or text like '%\(%'
or text like '%\)%'
or text like '%\-\-%'
or text like '%\=%'
or text like '%\>%'
or text like '%\<%'
or text like '%\;%'
or text like '%\:%'
or text like '%\"%'
or text like '%\'%'
or text like '%\,%'
or text like '%\?%'
or text like '%\½%'
or text like '%\|%'
or text like '%\}%'
or text like '%\{%'
or text like '%\+%'
or text like '%\/\/%'
or text like '%\/\_%'
or text like '%\_\/%'
or text like '%\_\_%'
or text like '%\_\.%'
or text like '%\/\\%'
or text like '%2001%'
or text like '%2002%'
or text like '%2003%'
or text like '%2004%'
or text like '%2005%'
or text like '%2006%'
or text like '%2007%'
or text like '%2008%'
or text like '%2009%'
or text like '%2010%'
or text like '%2011%'
or text like '%2012%'
or text like '%2013%'
or text like '%2014%'
or text like '%2015%'
or text like '%2016%'
or text like '% %'
or text like '%\/1\/%'
or text like '%\/2\/%'
or text like '%\/3\/%'
or text like '%\/4\/%'
or text like '%\/5\/%'
or text like '%\/6\/%'
or text like '%\/7\/%'
or text like '%\/8\/%'
or text like '%\/9\/%'
or text like '%\¿%'
or text like '%\±%'
or text like '%\¼%'
or text like '%\°%'
or text like '%\÷%'
or text like '%\»%'
or text like '%\.\.%'
or text like '%\.\/%'
or text like '%\\%'
```

**容易误伤的匹配**
```
or text like '%\-%'
or text like '%s8%'
or text like '%asked%'
or text like '%chufang%'
or text like '%chongzhi%'
or text like '%caiji%'
or text like '%bianji%'
or text like '%qingdao%'
or text like '%qqshopadmin%'
or text like '%ubb%'
or text like '%b2b%'
or text like '%cj\_%'
or text like '%ty\_%'
or text like '%p\-h%'
or text like '%ea\_c%'
or text like '%ds\_p%'
or text like '%in\_t%'
or text like '%min\_%'
or text like '%bs\_%'
or text like '%nf\_%'
or text like '%project\_2%'
or text like '%qzfyfs\_admin%'
or text like '%qwbm\_bookinc%'
or text like '%outward\_edit%'
or text like '%scs\_%'
or text like '%sdcms\_%'
or text like '%Fy\_Sql%'
or text like '%Gehang%'
or text like '%Guowai%'
or text like '%Gongye%'
or text like '%Keji%'
or text like '%Zuqiu%'
or text like '%Zixun%'
or text like '%amd\_007%'
or text like '%ewindowe%'
or text like '%jkxh%'
or text like '%xqfh%'
or text like '%lsjq%'
or text like '%zsbs%'
or text like '\/\.%'
or text like '%\/a\_%'
or text like '%\/b\_%'
or text like '%\/c\_%'
or text like '%\/m\_%'
or text like '%\/en\/%'
or text like '%\/zh\/%'
or text like '%\/excel2%'
or text like '%\/apsnetxml\/apsnetxml\/%'
or text like '%xinzhang%'
or text like '%xiaoshuo%'
or text like '%xmlbbs%'
or text like '%projectbbs%'
or text like '%zaoxue%'
or text like '%zhangkuan%'
or text like '%buymanage%'
or text like '%ztb\_bd\_%'
or text like '%admin\-%'
or text like '%deepsoo%'
or text like '%btoo\_%'
or text like '%forum\_%'
or text like '%gl\_%'
or text like '%global\_%'
or text like '%uyhut%'
or text like '%v3basic%'
or text like '%cdqh%'
or text like '%help\/help%'
or text like '%\/adminv612%'
or text like '%\/agent\/agent\/%'
or text like '%baobiao%'
or text like '%zxjwan%'
or text like '%xz\_%'
or text like '%dd\_%'
or text like '%\/alimnadmin%'
or text like '%\/cms\/cms%'
or text like '%headhunt%'
or text like '%wjgl%'
or text like '%\/jie%'
or text like '%job\_%'
or text like '%guangbo%'
or text like '%c000%'
or text like '%s000%'
or text like '%\/tpc00%'
or text like '%fckeditor1\_2%'
or text like '%jiao\_liu%'
or text like '%mbf\_user%'
or text like '%module\_article%'
or text like '%jizhang%'
or text like '%\/app_d\/%'
or text like '%visualtemplate%'
or text like '%\/membership\-%'
or text like '%第八天%'
or text like '%3\.5%'
or text like '%\/\.kins\/%'
or text like '%\/yonghua%'
or text like '%\/xuegong%'
or text like '%\/xjufida\_%'
or text like '%\/xiaoshou\_%'
or text like '%\/xhsqw_51%'
or text like '%\/wilsonwebformdemo%'
or text like '%\/website%'
or text like '%\/webform%'
or text like '%\/teach\_%'
or text like '%\/desktopmodules%'
or text like '%\/oaand%'
or text like '%\/membermanage%'
or text like '%z9v8%'
or text like '%\/manage\_%'
or text like '%\/loginstudent%'
or text like '%\/loginteacher%'
or text like '%\/iissamples%'
or text like '%\/safecode%'
or text like '%\/fesend%'
or text like '%\/english%'
or text like '%\_com%'
or text like '%accessories%'
or text like '%cx\_a%'
or text like '%app\_%'
or text like '%btoo\_%'
or text like '%xdrag\_ui%'
or text like '%wz\_%'
or text like '%xymanage%'
or text like '%yfhandler%'
or text like '%yxshop\.web%'
or text like '%zdymodel%'
or text like '%zdytag%'
or text like '%accessories%'
or text like '%ad\_%'
or text like '%\/bbs\/%'
or text like '%astreeiewdemo%'
or text like '%\/book\/%'
or text like '%\/chargemanage\/%'
or text like '%clientdependency\.web\.test%'
or text like '%\/clientmanage%'
or text like '%\/dengru%'
or text like '%\/dh\_%'
or text like '%company\_%'
or text like '%\/dotnettextboxwebsite%'
or text like '%\/cuteeditor%'
or text like '%\/hotelmanager%'
or text like '%\/dboperatorserice%'
or text like '%grid\_%'
or text like '%jiayi9%'
or text like '%057%'
or text like '%was5%'
or text like '%xiaoyuan%'
or text like '%tabbedpanel%'
or text like '%dianshi%'
or text like '%digshell%'
or text like '%dvbbs%'
or text like '%\/hl\/%'
or text like '%\/lyb\/%'
or text like '%fangchan%'
or text like '%pages2%'
or text like '%ylmf%'
or text like '%\_1%'
or text like '%\_2%'
or text like '%\_0%'
or text like '%\_3%'
or text like '%\_4%'
or text like '%\_5%'
or text like '%\_6%'
or text like '%\_7%'
or text like '%\_8%'
or text like '%\_9%'
or text like '%\/yq_%'
or text like '%\/zw_%'
or text like '%zuitu%'
or text like '%zwmobi%'
or text like '%zuitubiz%'
or text like '%\/z\_d%'
or text like '%\/Yz\_Plug%'
or text like '%\/yz\_qq%'
```
