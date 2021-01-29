FROM mochat/mochat:v1

RUN apk --no-cache add netcat-openbsd

COPY mc_init.phar /tmp/mc_init.phar
COPY wait-for /tmp/wait-for

RUN chmod o+x /tmp/wait-for

CMD sh -c "/tmp/wait-for mysql:3306 -- php /tmp/mc_init.phar"