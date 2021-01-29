# @mochat
FROM mochat/mochat:v1

ARG APP_ENV=production
ARG APP_NAME=mochat
ENV APP_ENV=${APP_ENV} \
    APP_NAME=${APP_NAME}

# 项目配置
WORKDIR /opt/www

# COPY . /opt/www
# RUN cd /opt/www && \
#     composer install --no-dev -o && \
#     php /opt/www/bin/hyperf.php
#
# ENTRYPOINT ["php", "/opt/www/bin/hyperf.php", "start"]

CMD sh -c "composer install && php /opt/www/bin/hyperf.php start"