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