

# 데이터베이스 사전 세팅

C:\Users\gonna>sqlplus / as sysdba

SQL*Plus: Release 21.0.0.0.0 - Production on 일 1월 18 23:14:07 2026
Version 21.3.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.


다음에 접속됨:
Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

PDB가 아닌 경우 전환
'''bash
SQL> show con_name;

CON_NAME
------------------------------
CDB$ROOT
SQL> ALTER SESSION SET "_ORACLE_SCRIPT" = true;

세션이 변경되었습니다.
'''

스키마가 없는 경우 스키마 생성
'''bash
SQL> CREATE USER ITPAPP IDENTIFIED BY "kdb1234!!";

사용자가 생성되었습니다.

SQL> GRANT CONNECT, RESOURCE, DBA TO ITPAPP;
'''


'''bash
SQL> CREATE OR REPLACE DIRECTORY my_dump_dir AS 'C:\it\it_database';

디렉토리가 생성되었습니다.

SQL> SELECT directory_name, directory_path FROM dba_directories WHERE directory_name = 'MY_DUMP_DIR';

DIRECTORY_NAME
--------------------------------------------------------------------------------
DIRECTORY_PATH
--------------------------------------------------------------------------------
MY_DUMP_DIR
C:\it\it_database

SQL> GRANT READ, WRITE ON DIRECTORY MY_DUMP_DIR TO ITPAPP;

권한이 부여되었습니다.
'''

# 가져오기
C:\it\it_database>impdp parfile=import.par

# 내보내기
C:\it\it_database>expdp parfile=export.par