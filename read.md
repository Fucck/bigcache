#问卷调查数据库设计

###用户表设计（questionnaire_user）

field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
open_id|int|NO||NULL|
session_key|int|NO||NULL|
avatar_url|varchar(512) |NO||NULL|
user_name|varchar(126)|NO||NULL|
mobile|int|NO||NULL|
is_banned|tinyint(1)|NO||0|
gender|tinyint(1)|NO||NULL|
language|varchar(126)|NO||NULL|
group|int|NO|MUL|NULL|
create_time|datetime|NO||NULL|CURRENT_TIMESTAMP
last_login|datetime|NO||NULL| CURRENT_TIMESTAMP

	用户表根据小程序开放接口文档设计：https://developers.weixin.qq.com/minigame/dev/api/open-api/user-info/UserInfo.html
	avatar_url为用户头像图片的url，is_banned为用户是否已被封禁
	group字段表示用户组，与组织表id相关联
	微信后台鉴权接口返回用户的openid和session_key用作鉴权

###权限表设计（）
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
role |tinyint(1)|NO||NULL|
authority|varchar(1024)|NO||NULL|
group|int|NO|MUL|NULL|
	group字段表示用户组，与组织表id相关联

###问卷表设计（questionnaire_questionnaire）
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
title|varchar(126)|NO||NULL|
sub_title|varchar(126)|NO||NULL|
description|varchar(1024)|NO||NULL|
creater|int|NO|MUL|NULL|
create_time|datetime|NO||NULL|CURRENT_TIMESTAMP
update_time|datetime|NO||NULL| CURRENT_TIMESTAMP
group|varchar(126)|NO|MUL|NULL|

	creater字段与用户表的用户id关联，group字段表示用户组，与组织表id相关联

###问卷—问题关联表（questionnaire_question_relate_paper）
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|
question_id|int|NO|MUL|NULL|
questionnaire_id|int|NO|MUL|NULL|
seq|int|NO||0|
	seq决定问题在问卷中的顺序

###问题表设计（questionnaire_question）
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
type|varchar(126)|NO||NULL|
content|varchar(126)|NO||NULL|
must_answer|tinyint(1)|NO||0|
create_time|datetime|NO||NULL|CURRENT_TIMESTAMP
update_time|datetime|NO||NULL| CURRENT_TIMESTAMP

	type说明问题类型
###问题-选项关联表(questionnaire_choice_relate_question)
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
choice_id|int|NO|MUL|NULL|
question_id|int|NO|MUL|NULL|
score|int|NO||0|
seq|int|NO||0|
	aid关联问题表的问题id；qid关联问题表的问题id；seq决定问题在问题中的顺序；score表示该选项在对应问题下的分数


###选项表设计(questionnaire_choice)
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
text|varchar(126)|NO||NULL|" "
create_time|datetime|NO||NULL|CURRENT_TIMESTAMP
update_time|datetime|NO||NULL| CURRENT_TIMESTAMP


###回答表设计(questionnaire_answers)
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
userid|int|NO|NUL|NULL|
chioce_set|varchar(1024)|NO||NULL|
create_time|datetime|NO||NULL|CURRENT_TIMESTAMP
update_time|datetime|NO||NULL| CURRENT_TIMESTAMP

	userid关联用户表的用户id；choice_set为用户对应问题-选项关联表id的集合

###组织表设计
field_name | type | null | key | default | extra
:-:|:-:|:-:|:-:|:-:|:-:|:-:
id|int|NO|pk|NULL|auto_increment
group|varchar(126)|NO||NULL|
create_time|datetime|NO||NULL|CURRENT_TIMESTAMP
update_time|datetime|NO||NULL| CURRENT_TIMESTAMP
