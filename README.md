# week-5
MySQL practice
### 要求三
* 使用 INSERT 指令新增一筆資料到 member 資料表中，這筆資料的 username 和 password 欄位必須是 test。接著繼續新增至少 4 筆隨意的資料。
```bash
insert into member(name, username, password, follower_count) value
('小春','test', 'test', 130);
insert into member(name, username, password, follower_count) value
('UU','uutest', 'uucode', 87),
('YY','yytest', 'yycode', 90),
('DUNKY','dtest', 'dcode', 88),
('GiantFish','Ftest', 'Fcode');
```
![]()
* 使用 SELECT 指令取得所有在 member 資料表中的會員資料。
```bash
select*from member;
```
![]()
* 使用 SELECT 指令取得所有在 member 資料表中的會員資料，並按照 time 欄位，由近到遠排序。
```bash
select* from member order by time desc;
```
![]()
* 使用 SELECT 指令取得 member 資料表中第 2 ~ 4 共三筆資料，並按照 time 欄位，由近到遠排序。( 並非編號 2、3、4 的資料，而是排序後的第 2 ~ 4 筆資料 )
```bash
select* from member order by time desc;
```
![]()
* 使用 SELECT 指令取得欄位 username 是 test 的會員資料。
```bash
select*from member where username='test';
```
![]()
* 使用 SELECT 指令取得欄位 username 是 test、且欄位 password 也是 test 的資料。
```bash
select*from member where username='test' and password='test';
```
![]()
* 使用 UPDATE 指令更新欄位 username 是 test 的會員資料，將資料中的 name 欄位改成 test2。
```bash
update member set name='test2' where username='test';
```
![]()



### 要求四

* 取得 member 資料表中，總共有幾筆資料 ( 幾位會員 )。
```bash
select count(*) from member;
```
![]()
* 取得 member 資料表中，所有會員 follower_count 欄位的總和。
```bash
select sum(follower_count) from member;
```
![]()
* 取得 member 資料表中，所有會員 follower_count 欄位的平均數。
```bash
select avg(follower_count) from member;
```
![]()



### 要求五

* 在資料庫中，建立新資料表紀錄留言資訊，取名字為 message。資料表中必須包含以下欄位設定:

  |欄位名稱 | 資料型態 | 額外設定             | 用途說明 |
  |----------|-------|--------------------|--------|
  |id        |bigint    |主鍵、自動遞增        | 獨立編號|
  |member_id | bigint  | 不可為空值 <br/>外鍵對應 member 資料表中的 id|留言者會員編號|
  |content  |varchar(255)|不可為空值          |留言內容 |
  |like_count |int unsigned|不可為空值，預設為 0|按讚的數量|
  |time      |datetime |不可為空值，預設為當前時間 |留言時間|
  
  ```bash
  create table message(
  id bigint primary key auto_increment comment '獨立編號', 
  member_id bigint not null comment '留言者會員編號', 
  content varchar(255) not null comment '留言內容', 
  like_count int unsigned not null default 0 comment '按讚的數量', 
  time datetime not null default current_timestamp comment '留言時間', 
  foreign key(member_id) references member(id)
  );
  ```
  ![]()
  
  * 使用 SELECT 搭配 JOIN 語法，取得所有留言，結果須包含留言者會員的姓名。
  ```bash
  select member.name, message.content 
  from member 
  inner join message 
  on member.id=message.member_id
  ;
  ```
  ![]()
  * 使用 SELECT 搭配 JOIN 語法，取得 member 資料表中欄位 username 是 test 的所有留言，資料中須包含留言者會員的姓名。
  ```bash
  select member.name, message.content 
  from member 
  inner join message 
  on member.username='test'and member.id=message.member_id
  ;
  ```
  ![]()
  * 使用 SELECT、SQL Aggregate Functions 搭配 JOIN 語法，取得 member 資料表中欄位 username 是 test 的所有留言平均按讚數。
  ```bash
  select member.username, avg(message.like_count) 
  from member 
  join message 
  on member.id=message.member_id 
  group by member.username 
  having member.username='test'
  ;
  ```
  ![]()




