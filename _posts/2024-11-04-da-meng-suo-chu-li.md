---
title: "达梦锁处理"
date: 2024-11-04 09:18:03 +0800
---

```sql
SELECT SYSDATE AS STATTIME,

       DATEDIFF(SS,S1.LAST_SEND_TIME,SYSDATE) AS SS，

       '被阻塞的信息' AS WT,

	   S1.SESS_ID AS WT_SESS_ID,

	   S1.SQL_TEXT AS WT_SQL_TEXT,

       S1.STATE AS WT_STATE,

	   S1.TRX_ID AS WT_TRX_ID,

	   S1.USER_NAME AS WT_USER_NAME, 

       S1.CLNT_IP AS WT_CLNT_IP,

	   S1.APPNAME AS WT_APPNAME,

	   S1.LAST_SEND_TIME AS WT_LAST_SEND_TIME,

	   '引起阻塞的信息' AS FM,

	   S2.SESS_ID AS FM_SESS_ID,

	   S2.SQL_TEXT AS FM_SQL_TEXT,

	   S2.STATE AS FM_STATE,

	   S2.TRX_ID AS FM_TRX_ID,

	   S2.USER_NAME AS FM_USER_NAME,

	   S2.CLNT_IP AS FM_CLNT_IP,

	   S2.APPNAME AS FM_APPNAME,

       S2.LAST_SEND_TIME AS FM_LAST_SEND_TIME

FROM V$SESSIONS S1，

V$SESSIONS S2 ,V$TRXWAIT W

WHERE S1.TRX_ID = W.ID

AND S2.TRX_ID = W.WAIT_FOR_ID;
```

```sql
当前活动连接数量太大说明业务量太大或者重连机制存在缺陷。

--查询当前所有会话数 

select count(*) from v$sessions; 

--查看当前数据库中活动会话

 select count(*) from v$sessions where state='ACTIVE'; 

--查看当前非活动会话 

select count(*) from v$sessions where state='IDLE';

--结束会话

sp_close_session(sessid);  --v$session中查出来的session id
```

```sql
select * from (

SELECT sess_id,sql_text,datediff(ss,last_recv_time,sysdate) Y_EXETIME,

       SF_GET_SESSION_SQL(SESS_ID) fullsql,clnt_ip

 FROM V$SESSIONS WHERE STATE='ACTIVE')

 where Y_EXETIME>=2;
```
