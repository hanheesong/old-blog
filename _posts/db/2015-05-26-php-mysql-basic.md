---
layout: amp
title: "[PHP] MySQL 함수"
description: "MySQL 함수 살펴보기"
tags: [ PHP, mysql, 데이터베이스 ]
category: db
sitemap:
  changefreq: daily
---

# 목차
- Mysql 함수
  * mysql_query()
  * mysql_num_rows()
  * mysql_num_fields()
  * mysql_fetch_row()
  * mysql_fetch_array()
  * mysql_result()

## mysql_query()
SQL 쿼리문을 실행하는 함수.
```sql
$sql = "";
$result = mysql_query($sql, $connect);
```

## mysql_num_rows()
**레코드 개수**가 몇 개인지 구하는 함수.
```sql
$sql = "select * from mem";
$result = mysql_query($sql, $connect);
$total_records = mysql_num_rows($result);
```

## mysql_num_fields()
**필드의 개수**가 몇 개인지 구하는 함수.
```sql
$sql = "select * from mem";
$result = mysql_query($sql, $connect);
$total_fields = mysql_num_fields($result);
```

## mysql_fetch_row()
[레코드집합](#레코드집합)에서 한 개의 **레코드값** 또는 **필드값**을 읽어오는 함수.
```php
<?php
  $connect = mysql_connect("localhost", "root", "1234");
  $db_con = mysql_select_db("sample", $connect );

  $sql="select * from mem";
  $result=mysql_query($sql,$connect);

  $fields=mysql_num_fields($result); //필드개수, $fields = 8
?>
<h2> mysql_fetch_row() 함수 예제</h2>
<table width=800 border=1 cellpadding=10>
  <tr>
    <td bgcolor=lightblue align=center>번호</td>
    <td bgcolor=lightblue align=center>아이디</td>
    <td bgcolor=lightblue align=center>이름</td>
    <td bgcolor=lightblue align=center>성별</td>
    <td bgcolor=lightblue align=center>우편번호</td>
    <td bgcolor=lightblue align=center>주소</td>
    <td bgcolor=lightblue align=center>전화번호</td>
    <td bgcolor=lightblue align=center>나이</td>
  </tr>
  <?php
    while ($row=mysql_fetch_row($result))
    {
      //8번 실행하고 실행할 때마다 하나씩 레코드를 가져와 배열 변수 $row에 저장함.
      echo ("<tr>");

      for ($i=0; $i < $fields; $i++)
      {
        echo ("<td> $row[$i]</td>");
      }
      echo ("</tr>");
    }
    mysql_close();
   ?>
</table>
```
## mysql_fetch_array
mysql_fetch_row()함수의 확장버전.
mysql_fetch_row()가 배열의 인덱스로써 필드의 일련번호를 사용했다면 mysql_fetch_array()함수는 $row[필드명]의 형태로 배열의 인덱스에 필드 이름을 직접 사용할 수 있다. 즉, $row[num], $row[name]... 이런식.

## mysql_result
mysql_fetch_row()나 mysql_fetch_array()나 하나의 레코드 값을 가져올 수 있는 것에 비해서 mysql_result()는 레코드값을 전부 가져올 수 있고, 3번째 인자인 필드의 일련번호 또는 필드명을 모두 사용할 수 있음.
```php
<?php
  $connect = mysql_connect("localhost", "root", "1234");
  $db_con = mysql_select_db("sample", $connect);

  $sql = "select * from mem";
  $result = mysql_query($sql, $connect);

  $records = mysql_num_rows($result);

  $fields = mysql_num_fields($result);

 ?>

 <h2> mysql_result() 함수 예제</h2>
 <table width=800 border=1 cellpadding=10>
   <tr>
     <td>번호</td>
     <td>아이디</td>
     <td>이름</td>
     <td>성별</td>
     <td>우편번호</td>
     <td>주소</td>
     <td>전화번호</td>
     <td>나이</td>
   </tr>
   <?php
    for ($i=0; $i < $records; $i++)
    {
        echo "<tr>";

        for ($j=0; $j < $fields; $j++)
        {
          $data = mysql_result($result, $i, $j);
          echo "<td> $data </td>";
        }

        echo "</tr>";
    }
    mysql_close();
    ?>
 </table>
```


- **레코드집합** : mysql_query()함수는 select문의 실행 결과로 레코드 집합(Resource ID)를 반환한다.



<a id="레코드집합"></a>
