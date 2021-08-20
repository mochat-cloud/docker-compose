# @mochat
FROM mochat/mochat:v1

ARG APP_ENV=production
ARG APP_NAME=mochat
ENV APP_ENV=${APP_ENV} \
    APP_NAME=${APP_NAME}

# 项目配置
WORKDIR /opt/www

# COPY ./ /opt/www
# RUN cd /opt/www && \
#     composer install --no-dev -o && \
#     php /opt/www/bin/hyperf.php

# ENTRYPOINT ["php", "/opt/www/bin/hyperf.php", "start"]

# 生产阶段使用以下配置
CMD sh -c "composer install -o && php /opt/www/bin/hyperf.php && php /opt/www/bin/hyperf.php start"

# 开发阶段使用以下配置，支持热更新
# CMD sh -c "composer install -o && php /opt/www/bin/hyperf.php && php /opt/www/bin/hyperf.php server:watch"
