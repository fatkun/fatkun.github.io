---
title: hibernate事务管理
author: fatkun
type: post
date: 2010-12-25T10:16:03+00:00
url: /2010/12/hibernate-transaction.html
duoshuo_thread_id:
  - 6300408796107768578
categories:
  - J2EE
  - 数据库
tags:
  - 数据库
  - 数据库事务
  - 隔离级别

---
## 1. 介绍数据库事务、事务隔离级别、悲观锁、乐观锁等概念。

## 2.数据库ACID特征：

> Atomic（原子性）：指整个数据库事务是不可分割的工作单元。
> Consistency（一致性）：指数据库事务不能破坏关系数据的完整性以及业务逻辑上的一致性。
> Isolation（隔离性）：指的是在并发环境中，当不同的事务同时操纵相同的数据时，每个事务都有各自的完整数据空间。
> Durability（持久性）：指的是只要事务成功结束，它对数据库所作的更新就必须永久保存下来。
## 3.数据库系统支持两种事务模式：

<p style="padding-left: 30px;">  自动提交模式：每个SQL语句都是一个独立的事务，当数据库系统执行完一个SQL语句后，会自动提交事务。</p>
<p style="padding-left: 30px;">  手动提交模式：必须由数据库客户程序显示指定事务开始边界和结束边界。</p>
## 4.MySQL中数据库表分为3种类型：

<p style="padding-left: 30px;">  INNODB、BDB和MyISAM，其中MyISAM不支持数据库事务。MySQL中create table 语句默认为MyISAM类型。</p>
## 5.并发问题

对于同时运行的多个事务，当这些事务访问数据库中相同的数据时，如果没有采取必要的隔离机制，就会导致各种并发问题，这些并发问题可归纳为以下几类：
> A.第一类丢失更新：撤销一个事务时，把其他事务已提交的更新数据覆盖。
> B.脏读：一个事务读到另一个事务为提交的更新数据。
> C.幻读：一个事务读到另一个事务已提交的新插入的数据。
> D.不可重复读：一个事务读到另一个事务已提交的更新数据。
> E.第二类丢失更新：这是不可重复读中的特例，一个事务覆盖另一个事务已提交的更新数据。
## 6.数据库系统四种事务隔离级别

<p style="padding-left: 30px;">  A.Serializable（串行化）：一个事务在执行过程中完全看不到其他事务对数据库所做的更新。</p>
<p style="padding-left: 30px;">  B.Repeatable Read（可重复读）：一个事务在执行过程中可以看到其他事务已经提交的新插入的记录，但是不能看到其他其他事务对已有记录的更新。</p>
<p style="padding-left: 30px;">  C.Read Commited（读已提交数据）：一个事务在执行过程中可以看到其他事务已经提交的新插入的记录，而且能看到其他事务已经提交的对已有记录的更新。</p>
<p style="padding-left: 30px;">  D.Read Uncommitted（读未提交数据）：一个事务在执行过程中可以拷打其他事务没有提交的新插入的记录，而且能看到其他事务没有提交的对已有记录的更新。</p>
<table border="1" cellspacing="0" cellpadding="0" width="576">  <tr>    <td width="164">      <div>        隔离级别      </div>    </td>
    <td width="82">      <div>        脏读      </div>    </td>
    <td width="82">      <div>        不可      </div>
      <div>        重复读      </div>    </td>
    <td width="82">      <div>        幻象读      </div>    </td>
    <td width="82">      <div>        第一类丢失更新      </div>    </td>
    <td width="82">      <div>        第二类丢失更新      </div>    </td>  </tr>
  <tr>    <td width="164" valign="top">      <div>        READ UNCOMMITED      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>  </tr>
  <tr>    <td width="164" valign="top">      <div>        READ COMMITTED      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>  </tr>
  <tr>    <td width="164" valign="top">      <div>        REPEATABLE READ      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>  </tr>
  <tr>    <td width="164" valign="top">      <div>        SERIALIZABLE      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>
    <td width="82">      <div>        不允许      </div>    </td>  </tr></table>
<p style="padding-left: 30px;">  隔离级别越高，越能保证数据的完整性和一致性，但是对并发性能的影响也越大。对于多数应用程序，可以有优先考虑把数据库系统的隔离级别设为Read Commited，它能够避免脏读，而且具有较好的并发性能。尽管它会导致不可重复读、幻读和第二类丢失更新这些并发问题，在可能出现这类问题的个别场合，可以由应用程序采用悲观锁或乐观锁来控制。</p>
## 7.当数据库系统采用read Commited隔离级别时

会导致不可重复读喝第二类丢失更新的并发问题，可以在应用程序中采用悲观锁或乐观锁来避免这类问题。从应用程序的角度，锁可以分为以下几类：
<p style="padding-left: 30px;">  A.悲观锁：指在应用程序中显示的为数据资源加锁。尽管能防止丢失更新和不可重复读这类并发问题，但是它会影响并发性能，因此应该谨慎地使用。</p>
<p style="padding-left: 30px;">  B.乐观锁：乐观锁假定当前事务操作数据资源时，不回有其他事务同时访问该数据资源，因此完全依靠数据库的隔离级别来自动管理锁的工作。应用程序采用版本控制手段来避免可能出现的并发问题。</p>
## 8.悲观锁有两种实现方式：

<p style="padding-left: 30px;">  A.在应用程序中显示指定采用数据库系统的独占所来锁定数据资源。SQL语句：select &#8230; for update，在Hibernate中使用get，load时如session.get(Account.class,new Long(1),LockMode,UPGRADE)</p>
<p style="padding-left: 30px;">  B.在数据库表中增加一个表明记录状态的LOCK字段，当它取值为“Y”时，表示该记录已经被某个事务锁定，如果为“N”，表明该记录处于空闲状态，事务可以访问它。增加锁标记字段就可以实现。</p>
## 9.利用Hibernate的版本控制来实现乐观锁

<p style="padding-left: 30px;">  乐观锁是由程序提供的一种机制，这种机制既能保证多个事务并发访问数据，又能防止第二类丢失更新问题。</p>
<p style="padding-left: 30px;">  在应用程序中可以利用Hibernate提供的版本控制功能来视线乐观锁，OR映射文件中的<version>元素和<timestamp>都具有版本控制的功能，一般推荐采用<version></p>
本文来源：<http://blog.csdn.net/yueguangyuan/archive/2006/09/20/1253229.aspx>