---
layout: post
title: "Postgresql"
description: 
headline: 
modified: 2020-03-26
category: webdevelopment
imagefeature: cover3.jpg
tags: [Postgresql]
mathjax: 
chart: 
share: true
comments: true
featured: false
disqus:
---
# Postgresql


## lock 해소
```JavaScript

select * from pg_catalog.pg_locks

select * from pg_catalog.pg_locks a, pg_catalog.pg_stat_all_tables b where a.relation = b.relid

select * from pg_catalog.pg_stat_activity

select pg_cancel_backend(31129);

select pg_terminate_backend(31129) from pg_stat_activity


```

## PostgreSQL Exception handling detail with GET STACKED DIAGNOSTICS

```JavaScript
    CREATE OR REPLACE FUNCTION test(INT4) RETURNS void as $$
    DECLARE
        v_state   TEXT;
        v_msg     TEXT;
        v_detail  TEXT;
        v_hint    TEXT;
        v_context TEXT;
    BEGIN

        BEGIN
            INSERT INTO test2 (id) VALUES ($1);
        EXCEPTION WHEN others THEN
            GET STACKED DIAGNOSTICS
                v_state   = RETURNED_SQLSTATE,
                v_msg     = MESSAGE_TEXT,
                v_detail  = PG_EXCEPTION_DETAIL,
                v_hint    = PG_EXCEPTION_HINT,
                v_context = PG_EXCEPTION_CONTEXT;
            raise notice E'Got exception:
                state  : %
                message: %
                detail : %
                hint   : %
                context: %', v_state, v_msg, v_detail, v_hint, v_context;
        END;
        RETURN;
    END;
    $$ language PLpgSQL;
```




## Use RAISE Statements to debug

```JavaScript

RAISE level format;
 DEBUG
 LOG
 NOTICE
 INFO
 WARNING
 EXCEPTION

    DO $$ 
    BEGIN 
    RAISE INFO 'information message %', now() ;
    RAISE LOG 'log message %', now();
    RAISE DEBUG 'debug message %', now();
    RAISE WARNING 'warning message %', now();
    RAISE NOTICE 'notice message %', now();
    END $$;

USING option = expression
 MESSAGE: set error message text
 HINT: provide the hint message so that the root cause of the error is easier to be discovered.
 DETAIL:  give detailed information about the error.
 ERRCODE: identify the error code, which can be either by condition name or directly five-character SQLSTATE code. Please refer to the table of error codes and condition names.

    DO $$ 
    DECLARE
    email varchar(255) := 'info@postgresqltutorial.com';
    BEGIN 
    -- check email for duplicate
    -- ...
    -- report duplicate email
    RAISE EXCEPTION 'Duplicate email: %', email 
        USING HINT = 'Check the email again';
    END $$;

    DO $$ 
    BEGIN 
    --...
    RAISE SQLSTATE '2210B';
    END $$;

    CREATE OR REPLACE FUNCTION msgfailerror() 
    RETURNS trigger AS 
    $$
    BEGIN 
    IF NEW.noces< new.first_column THEN 
        RAISE EXCEPTION 'cannot have a negative salary'; 
    END IF; 
    return new; 
    END;
    $$
    LANGUAGE plpgsql;    
```


## Procedures and transaction control

```JavaScript
CREATE PROCEDURE transaction_test1()
LANGUAGE plpgsql
AS $$
BEGIN
    FOR i IN 0..9 LOOP
        INSERT INTO test1 (a) VALUES (i);
        IF i % 2 = 0 THEN
            COMMIT;
        ELSE
            ROLLBACK;
        END IF;
    END LOOP;
END
$$;

CALL transaction_test1();
```


## postgresql ORA-08177: can't serialize access for this transaction
```JavaScript
    *** SEGMENT CREATION IMMEDIATE; 

    CREATE TABLE scott.gis (
        id  NUMBER(5) PRIMARY KEY,
        g   MDSYS.SDO_GEOMETRY
    ) SEGMENT CREATION IMMEDIATE;

```



## lock 테이블 확인 

select t.relname,l.locktype,page,virtualtransaction,pid,mode,granted  
from pg_locks l, pg_stat_all_tables t 
where l.relation=t.relid order by relation asc; 

## lock 삭제 

select pg_cancel_backend(pid);

## Postgres connection has been closed error in Spring Boot
- org.springframework.jdbc.support.MetaDataAccessException: Error while extracting DatabaseMetaData; nested exception is org.postgresql.util.PSQLException: This connection has been closed.

- Option 1: Toss out broken connections from the pool.

spring.datasource.test-on-borrow=true
spring.datasource.validation-query=SELECT 1;
spring.datasource.validation-interval=30000

- Option 2: Keep connections in the pool alive.

spring.datasource.test-while-idle=true
spring.datasource.validation-query=SELECT 1;
spring.datasource.time-between-eviction-runs-millis=60000

- Option 3: Proactively toss out idle connections.

spring.datasource.remove-abandoned=true
spring.datasource.remove-abandoned-timeout=60


```JavaScript

[INFO ] 2020-05-08 13:32:21.870 [pool-2-thread-84] OwnerFlowThread - START Postgressql From Oracle 1:32:21.870
[INFO ] 2020-05-08 13:32:41.198 [pool-2-thread-84] XmlBeanDefinitionReader - Loading XML bean definitions from class path resource [org/springframework/jdbc/support/sql-error-codes.xml]
[INFO ] 2020-05-08 13:32:41.611 [pool-2-thread-84] SQLErrorCodesFactory - SQLErrorCodes loaded: [DB2, Derby, H2, HSQL, Informix, MS-SQL, MySQL, Oracle, PostgreSQL, Sybase, Hana]
[WARN ] 2020-05-08 13:32:41.611 [pool-2-thread-84] SQLErrorCodesFactory - Error while extracting database name - falling back to empty error codes
org.springframework.jdbc.support.MetaDataAccessException: Error while extracting DatabaseMetaData; nested exception is org.postgresql.util.PSQLException: This connection has been closed.
	at org.springframework.jdbc.support.JdbcUtils.extractDatabaseMetaData(JdbcUtils.java:342) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.JdbcUtils.extractDatabaseMetaData(JdbcUtils.java:366) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.SQLErrorCodesFactory.getErrorCodes(SQLErrorCodesFactory.java:212) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.SQLErrorCodeSQLExceptionTranslator.setDataSource(SQLErrorCodeSQLExceptionTranslator.java:134) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.SQLErrorCodeSQLExceptionTranslator.<init>(SQLErrorCodeSQLExceptionTranslator.java:97) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.JdbcAccessor.getExceptionTranslator(JdbcAccessor.java:99) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:419) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:443) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]

Caused by: org.postgresql.util.PSQLException: This connection has been closed.
	at org.postgresql.jdbc.PgConnection.checkClosed(PgConnection.java:803) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgConnection.getMetaData(PgConnection.java:1268) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]

[ERROR] 2020-05-08 13:32:41.978 [pool-2-thread-84] TaskUtils$LoggingErrorHandler - Unexpected error occurred in scheduled task.
org.springframework.dao.DataAccessResourceFailureException: StatementCallback; SQL [call sp_postgresql_from_oracle()]; An I/O error occurred while sending to the backend.; nested exception is org.postgresql.util.PSQLException: An I/O error occurred while sending to the backend.
	at org.springframework.jdbc.support.SQLStateSQLExceptionTranslator.doTranslate(SQLStateSQLExceptionTranslator.java:105) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:73) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:81) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:81) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:419) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:443) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]

Caused by: org.postgresql.util.PSQLException: An I/O error occurred while sending to the backend.
	at org.postgresql.core.v3.QueryExecutorImpl.execute(QueryExecutorImpl.java:314) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgStatement.executeInternal(PgStatement.java:430) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgStatement.execute(PgStatement.java:356) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgStatement.executeWithFlags(PgStatement.java:303) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgStatement.executeCachedSql(PgStatement.java:289) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgStatement.executeWithFlags(PgStatement.java:266) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgStatement.execute(PgStatement.java:262) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]

Caused by: java.net.SocketException: Software caused connection abort: recv failed
	at java.net.SocketInputStream.socketRead0(Native Method) ~[?:1.8.0_74]
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116) ~[?:1.8.0_74]
	at java.net.SocketInputStream.read(SocketInputStream.java:170) ~[?:1.8.0_74]
	at java.net.SocketInputStream.read(SocketInputStream.java:141) ~[?:1.8.0_74]
	at org.postgresql.core.VisibleBufferedInputStream.readMore(VisibleBufferedInputStream.java:140) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.core.VisibleBufferedInputStream.ensureBytes(VisibleBufferedInputStream.java:109) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.core.VisibleBufferedInputStream.read(VisibleBufferedInputStream.java:67) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.core.PGStream.receiveChar(PGStream.java:280) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.core.v3.QueryExecutorImpl.processResults(QueryExecutorImpl.java:1916) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.core.v3.QueryExecutorImpl.execute(QueryExecutorImpl.java:288) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]


[INFO ] 2020-05-08 13:32:46.717 [pool-2-thread-24] OwnerFlowThread - START Postgressql Thread 1:32:46.717
[WARN ] 2020-05-08 13:32:46.781 [pool-2-thread-24] SQLErrorCodesFactory - Error while extracting database name - falling back to empty error codes
org.springframework.jdbc.support.MetaDataAccessException: Error while extracting DatabaseMetaData; nested exception is org.postgresql.util.PSQLException: This connection has been closed.
	at org.springframework.jdbc.support.JdbcUtils.extractDatabaseMetaData(JdbcUtils.java:342) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.JdbcUtils.extractDatabaseMetaData(JdbcUtils.java:366) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.SQLErrorCodesFactory.getErrorCodes(SQLErrorCodesFactory.java:212) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.SQLErrorCodeSQLExceptionTranslator.setDataSource(SQLErrorCodeSQLExceptionTranslator.java:134) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.SQLErrorCodeSQLExceptionTranslator.<init>(SQLErrorCodeSQLExceptionTranslator.java:97) [spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]

Caused by: org.postgresql.util.PSQLException: This connection has been closed.
	at org.postgresql.jdbc.PgConnection.checkClosed(PgConnection.java:803) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgConnection.getMetaData(PgConnection.java:1268) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]

[ERROR] 2020-05-08 13:32:46.796 [pool-2-thread-24] TaskUtils$LoggingErrorHandler - Unexpected error occurred in scheduled task.
org.springframework.dao.DataAccessResourceFailureException: 
### Error querying database.  Cause: org.postgresql.util.PSQLException: This connection has been closed.
### The error may exist in file [C:\egovframeworkSample\eclipse-jee-neon-2-win32-x86_64\workspace\klnet.owner.Schedule\target\classes\mappers\postgresql\OwnerMapper.xml]
### The error may involve com.klnet.owner.selectPostgresqlThread
### The error occurred while executing a query
### Cause: org.postgresql.util.PSQLException: This connection has been closed.
; SQL []; This connection has been closed.; nested exception is org.postgresql.util.PSQLException: This connection has been closed.
	at org.springframework.jdbc.support.SQLStateSQLExceptionTranslator.doTranslate(SQLStateSQLExceptionTranslator.java:105) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:73) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:81) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:81) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]


Caused by: org.postgresql.util.PSQLException: This connection has been closed.
	at org.postgresql.jdbc.PgConnection.checkClosed(PgConnection.java:803) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgConnection.getAutoCommit(PgConnection.java:764) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]

[INFO ] 2020-05-08 13:34:08.318 [pool-2-thread-85] OwnerFlowThread - START Postgressql From Oracle2 1:34:8.318
[ERROR] 2020-05-08 13:34:08.318 [pool-2-thread-85] TaskUtils$LoggingErrorHandler - Unexpected error occurred in scheduled task.
org.springframework.dao.DataAccessResourceFailureException: StatementCallback; SQL [call sp_postgresql_from_oracle2()]; This connection has been closed.; nested exception is org.postgresql.util.PSQLException: This connection has been closed.
	at org.springframework.jdbc.support.SQLStateSQLExceptionTranslator.doTranslate(SQLStateSQLExceptionTranslator.java:105) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:73) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:81) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:81) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:419) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]
	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:443) ~[spring-jdbc-4.3.10.RELEASE.jar:4.3.10.RELEASE]

Caused by: org.postgresql.util.PSQLException: This connection has been closed.
	at org.postgresql.jdbc.PgConnection.checkClosed(PgConnection.java:803) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgConnection.createStatement(PgConnection.java:1615) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]
	at org.postgresql.jdbc.PgConnection.createStatement(PgConnection.java:410) ~[postgresql-9.4.1212.jre7.jar:9.4.1212.jre7]


```



##  Foreign Data Wrapper for Oracle
CREATE FOREIGN TABLE oratab (
              id        integer           OPTIONS (key 'true')  NOT NULL,
              text      character varying(30),
              floating  double precision  NOT NULL
           ) SERVER oradb OPTIONS (schema 'ORAUSER', table 'ORATAB');
