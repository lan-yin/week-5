# week-5
MySQL practice
### 要求三
* 使用 INSERT 指令新增一筆資料到 member 資料表中，這筆資料的 username 和 password 欄位必須是 test。接著繼續新增至少 4 筆隨意的資料。
```bash
insert into member(name, username, password, follower_count) value
('小春','test', 'test', 130);
```
<img width="726" alt="3-1" src="https://user-images.githubusercontent.com/64936442/196651322-d0e46f33-624b-4f3f-9ece-f0359ca2282f.png">


```bash
insert into member(name, username, password, follower_count, time) value
('UU','uutest', 'uucode', 87, '2022-10-15 16:55:14'),
('YY','yytest', 'yycode', 90, '2022-10-15 13:55:14'),
('DUNKY','dtest', 'dcode', 88, '2022-10-20 16:55:14'),
('GiantFish','Ftest', 'Fcode', 67, '2022-10-10 16:55:14')
;
```
<img width="736" alt="3-1-1" src="https://user-images.githubusercontent.com/64936442/196650929-e49cc86a-5472-42f8-8927-3ffb5ccf920e.png">

* 使用 SELECT 指令取得所有在 member 資料表中的會員資料。
```bash
select*from member;
```
<img width="749" alt="3-2" src="https://user-images.githubusercontent.com/64936442/196651441-e8f92a85-4880-4aaa-9b43-0b190c1948c2.png">


* 使用 SELECT 指令取得所有在 member 資料表中的會員資料，並按照 time 欄位，由近到遠排序。
```bash
select* from member order by time desc;
```
<img width="741" alt="3-3" src="https://user-images.githubusercontent.com/64936442/196651558-53430a78-29bb-45e6-99ac-6041b2cccd0b.png">


* 使用 SELECT 指令取得 member 資料表中第 2 ~ 4 共三筆資料，並按照 time 欄位，由近到遠排序。( 並非編號 2、3、4 的資料，而是排序後的第 2 ~ 4 筆資料 )
```bash
select*from member order by time desc limit 1,3;
```
<img width="718" alt="3-4" src="https://user-images.githubusercontent.com/64936442/196651612-d6cbc4f2-665b-4f6e-895b-a9af4ba28952.png">


* 使用 SELECT 指令取得欄位 username 是 test 的會員資料。
```bash
select*from member where username='test';
```
<img width="745" alt="3-5" src="https://user-images.githubusercontent.com/64936442/196651653-b673d809-12c0-4f59-af81-609be990cdf4.png">


* 使用 SELECT 指令取得欄位 username 是 test、且欄位 password 也是 test 的資料。
```bash
select*from member where username='test' and password='test';
```
<img width="724" alt="3-6" src="https://user-images.githubusercontent.com/64936442/196651728-34db91c1-170a-447d-b585-874733ba5a12.png">


* 使用 UPDATE 指令更新欄位 username 是 test 的會員資料，將資料中的 name 欄位改成 test2。
```bash
update member set name='test2' where username='test';
```
<img width="695" alt="3-7" src="https://user-images.githubusercontent.com/64936442/196651748-031ab734-d8cf-424a-94f7-68c4d5303478.png">



### 要求四

* 取得 member 資料表中，總共有幾筆資料 ( 幾位會員 )。
```bash
select count(*) from member;
```
<img width="369" alt="4-1" src="https://user-images.githubusercontent.com/64936442/196651939-d6dafefb-7284-4bf8-96ee-9d147f99f071.png">


* 取得 member 資料表中，所有會員 follower_count 欄位的總和。
```bash
select sum(follower_count) from member;
```
<img width="452" alt="4-2" src="https://user-images.githubusercontent.com/64936442/196651985-d4988c21-5df9-4a8e-8727-da7cbb1430e8.png">


* 取得 member 資料表中，所有會員 follower_count 欄位的平均數。
```bash
select avg(follower_count) from member;
```
<img width="465" alt="4-3" src="https://user-images.githubusercontent.com/64936442/196652007-ba5d3e0c-4b06-4f2a-afbc-1eb09f32c049.png">




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
 <img width="723" alt="5-0" src="https://user-images.githubusercontent.com/64936442/196652366-c4b8dbcd-b008-457f-823b-9b7f71f92653.png">

 
 
  
  * 使用 SELECT 搭配 JOIN 語法，取得所有留言，結果須包含留言者會員的姓名。
  ```bash
  select member.name, message.content 
  from member 
  inner join message 
  on member.id=message.member_id
  ;
  ```
 <img width="414" alt="5-1" src="https://user-images.githubusercontent.com/64936442/196652403-a269a2c6-2cfb-429d-99bc-f7aa4d5546d1.png">

 
 
  * 使用 SELECT 搭配 JOIN 語法，取得 member 資料表中欄位 username 是 test 的所有留言，資料中須包含留言者會員的姓名。
  ```bash
  select member.name, message.content 
  from member 
  inner join message 
  on member.username='test'and member.id=message.member_id
  ;
  ```
 <img width="613" alt="5-2" src="https://user-images.githubusercontent.com/64936442/196652437-a9981a68-9a5f-4547-b3f4-8f42a65888ce.png">

 
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
<img width="515" alt="5-3" src="https://user-images.githubusercontent.com/64936442/196652458-45ae4b17-b9b4-4703-9828-b0353ab508e5.png">





