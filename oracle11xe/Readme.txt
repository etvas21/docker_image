ref: https://www.sysnet.pe.kr/2/0/12191
user: system, password:oracle

docker pull oracleinanutshell/oracle-xe-11g


docker run -p 1521:1521 oracleinanutshell/oracle-xe-11g
    docker run --name oraclexe1 -d -p 1521:1521 oracleinanutshell/oracle-xe-11g
    docker run --name oraclexe1 -d -p 1521:1521 --restart=always oracleinanutshell/oracle-xe-11g


#    docker run --name oraclexe1 -p 1521:1521 -v oracle11g_root:/u01/app/oracle oracleinanutshell/oracle-xe-11g

#    docker run --name ora11gxe -p 1521:1521 -v vol_ora11gxe:/u01/app/oracle oracleinanutshell/oracle-xe-11g

# docker run --name ora11gxe -p 1521:1521 -v d:\_database\docker_volume\vol_ora11gxe:/u01/app/oracle oracleinanutshell/oracle-xe-11g


# docker run --name ora11gxe -p 1521:1521 -e ORACLE_ALLOW_REMOTE=true -v d:\_database\docker_volume\vol_ora11gxe:/u01/app/oracle/oradata/XE --restart=always oracleinanutshell/oracle-xe-11g

# 직접 repository를 지정하니 error 발생하여
# docker volume create vol_ora11g로 생성을 하여 실행하니 OK

docker run --name ora11gxe -p 1521:1521 -e ORACLE_ALLOW_REMOTE=true -v vol_ora11g:/u01/app/oracle/oradata/XE --restart=always oracleinanutshell/oracle-xe-11g