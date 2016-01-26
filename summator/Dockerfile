FROM busybox

RUN echo 'while true ; do  { echo -ne "HTTP/1.0 200 OK\r\n\r\n"; wget -O- http://$SAY_HELLO_HOST:$SAY_HELLO_PORT; wget -O- http://$SAY_WORLD_HOST:$SAY_WORLD_PORT;  } | nc -l -p 80  || break; done' > /etc/cmd.sh

RUN chmod +x /etc/cmd.sh

CMD ["/bin/sh", "/etc/cmd.sh"]