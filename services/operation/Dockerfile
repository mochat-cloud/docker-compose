# @mochat
FROM node:14.17.3 AS build

RUN yarn config set registry https://registry.npm.taobao.org

# 编译目录设置
WORKDIR /opt/www

# # 拷贝代码
# COPY . /opt/www
# # 代码编译
# RUN yarn install && yarn run build
# # nginx镜像
# FROM nginx
# #引入build阶段编译的静态文件
# COPY --from=build /opt/www/dist/ /opt/www/operation/dist/
# # 暴露端口
# EXPOSE 80

# dev
CMD sh -c "yarn install && yarn run build"
