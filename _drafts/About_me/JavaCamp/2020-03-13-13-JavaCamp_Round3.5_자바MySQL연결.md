---
layout: post
title: "[Java-GUI] ROUND3. 번외 ) MySQL 설치 및 Eclipse Java - MySQL 연동"
date: 2020-03-14
categories: JavaCamp
tags: about java gui database mysql
sitemap:
    changefreq: daily
---

프로젝트의 번외편으로 자바로 MySQL을 연동시키는 방법에 대해 이야기 하려한다. 나도 프로젝트를 진행할 당시에 데이터베이스에 대한 개념이 없어 힘들었던 기억이 있기 때문에... 본 포스팅은 eclipse에서 자바와 MySQL을 연동시킬 수 있는 간단한 방법에 대해 이야기한다.   
<br/>

## 1. MySQL connector/J 다운로드
<https://dev.mysql.com/downloads/connector/j/>  

위 사이트에서 MySQL connector/J를 다운받는다.  
Operating System은 <span style="color: #c70000">Platform Independent</span>를 선택하고 <span style="color: #c70000">ZIP</span> 파일을 다운 받는다.  
해당 파일의 압축을 풀어 mysql-connector-java-8.0.11.jar 파일이 있는 것을 확인한다.
<br/><br/><br/>

## 2. MySQL 다운로드
<https://dev.mysql.com/downloads/mysql/>  

위 사이트에서 MySQL을 다운 받는다.  
Operating System은 자신의 컴퓨터에 맞는 OS를 선택한다.  
또한 <span style="color: #c70000">Window는 ZIP</span> 파일을, <span style="color: #c70000">macOS는 DMG</span> 파일을 다운 받는다.  
설치 도중에 비밀번호를 입력하는 과정이 있을텐데 이때의 비밀번호는 잘 기억해둬야 한다.  
다운로드 과정이 복잡해서 어려운 사람들은 아래 블로그를 참고하면 좋을 것 같다.  
Window : <https://dog-developers.tistory.com/20>,  
macOS : <https://daimhada.tistory.com/121>  
다운 받은 파일은 압축을 풀어 준비한다.
<br/><br/><br/>

## 3. MySQL 서버 실행
MySQL 다운로드에서 블로그를 참고해서 다운받았던 사람들은 이 과정을 넘겨도 무방하며,  
MySQL 서버를 실행시킨 상태로 두고 다음 단계로 넘어가면 된다.  

이제 다운로드는 마쳤으니 MySQL 서버를 실행시켜 Database를 사용할 준비를 해야한다.  
MySQL을 다운 받아 압축을 풀었던 폴더로 이동해서 <span style="color: #c70000">Window는 cmd</span>를, <span style="color: #c70000">macOS는 터미널</span>을 실행시킨다.  
해당 폴더 안의 bin 폴더로 들어가 mysql을 실행시킨다.  

<br/>
Window의 경우 해당 폴더에서 cmd를 실행시켜 아래 명령어를 이용하면 된다.  

```
cd bin
mysql.exe --initialize
mysqld --console --explicit_defaults_for_timestamp --skip-grant-tables &

// 새로운 cmd를 켜서 다시 bin 폴더로 이동 및 mysql 실행
cd bin
mysql -u root mysql
```
<br/>
macOS의 경우 해당 폴더에서 터미널을 실행시켜 아래 명령어를 이용하면 된다.

```
cd bin
./mysql -u root -p
```
<br/>

만약 위 과정이 잘 되지 않거나 어렵다면, 아래 블로그를 참고하면 좋을 것 같다.    
Window : <https://dog-developers.tistory.com/20>  
macOS : <https://daimhada.tistory.com/121>
<br/><br/><br/>

## 4. MySQL database, table 생성
MySQL은 다운받고 실행시켰지만 다음으로 MySQL 데이터 베이스를 사용하기 위한 준비 과정이 필요하다.  
바로 데이터베이스와 테이블, 칼럼을 생성시키는 과정이다.  

이 과정은 아래 블로그를 참고하면 좋을 것 같다.  
<https://futurists.tistory.com/11?category=587334wkqkhttp://futurists.tistory.com/11?category=587334>
<br/><br/><br/>

## 5. Java - MySQL 연동
드디어 모든 준비가 마쳤다.  
이제 Eclipse를 사용해서 Java와 MySQL을 연동시켜보자.  

1) Eclipse에서 MySQL과 연동할 Java 프로젝트를 생성한다.  
2) 해당 프로젝트 '우클릭 - Build Path - Add External Archives' 를 선택한다.  
3) 처음에 다운 받았던 mysql-connector-java-8.0.11.jar 파일을 추가한다.  
4) 아래 코드를 이용해서 주석 부분을 잘 보고 수정해야할 부분은 수정한 뒤 실행시켜 MySQL과 연동이 되었는지 확인한다.  
5) 코드의 실행 결과로 "연결완료"라고 프린트 된다면 성공적으로 연결된 것이다!

<br/>

```java
package java.database; // 패키지명 수정

import java.sql.*;
import java.io.*;

public class MysqlConnection{
	Connection conn = null;
	Statement stmt = null;
	PreparedStatement pstmt = null;
	ResultSet rs = null;

	MysqlConnection() {
		Try {
			Class.forName("com.mysql.cj.jdbc.Driver").newInstance(); // JDBC 드라이버 로드
			conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/[table name]?serverTimezone=UTC&&useSSL=false", "root", "[pwd]"); // []부분 ([table name], [pwd]) 수정
			System.out.println(“연결 완료”);
		}catch(ClassNotFoundException ce){
			ce.printStackTrace();
		}catch(SQLException se){
			se.printStackTrace();
		}catch(Exception e){
			e.printStackTrace();
		}finally{
			try{ // 연결 해제(한정돼 있으므로)
				if(rs!=null){rs.close();}
				if(pstmt!=null){pstmt.close();}
				if(stmt!=null){stmt.close();}
				if(conn!=null){conn.close();}
			}catch(SQLException se2){
				se2.printStackTrace();
			}
		}
	}
}
```
<br/><br/>