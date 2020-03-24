ref: https://www.sysnet.pe.kr/2/0/12191

docker pull oracleinanutshell/oracle-xe-11g


docker run -p 1521:1521 oracleinanutshell/oracle-xe-11g
    docker run --name oraclexe1 -d -p 1521:1521 oracleinanutshell/oracle-xe-11g
    docker run --name oraclexe1 -d -p 1521:1521 --restart=always oracleinanutshell/oracle-xe-11g


    docker run --name oraclexe1 -p 1521:1521 -v oracle11g_root:/u01/app/oracle oracleinanutshell/oracle-xe-11g
