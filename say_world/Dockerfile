FROM busybox

RUN echo 'while true ; do  { echo -ne "HTTP/1.0 200 OK\r\n\r\n"; echo -n "world!";  } | nc -l -p 80  || break; done' > /etc/cmd.sh

RUN chmod +x /etc/cmd.sh

CMD ["/bin/sh", "/etc/cmd.sh"]