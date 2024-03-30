# 使用 pokerhub服务器基础镜像作为基础镜像
FROM pokerhub:server_base.v1

# 设置工作目录为 /root
WORKDIR /root

# 将当前目录下的所有文件复制到容器的 /root 目录
COPY server /root/server/.

# 切换到 /root/server/skynet 目录，执行相关命令
WORKDIR /root/server/skynet
RUN chmod +x /root/server/skynet/3rd/jemalloc/*.sh \
    && dos2unix /root/server/skynet/3rd/jemalloc/*.sh \
    #&& dos2unix /root/server/skynet/3rd/jemalloc/include/*.sh \
    && dos2unix /root/server/skynet/3rd/jemalloc/include/jemalloc/*.sh \
    && chmod +x /root/server/skynet/3rd/jemalloc/include/jemalloc/*.sh \
    && dos2unix /root/server/skynet/3rd/jemalloc/include/jemalloc/internal/*.sh \
    && chmod +x /root/server/skynet/3rd/jemalloc/include/jemalloc/internal/*.sh \
    && make linux

# 切换回 /root/server 目录，执行相关命令
WORKDIR /root/server
RUN chmod +x /root/server/tools/*.sh \
    && dos2unix /root/server/tools/*.sh \
    && chmod +x /root/server/shell/*.sh \
    && dos2unix /root/server/shell/*.sh \
    && chmod +x /root/server/*.sh \
    && dos2unix /root/server/*.sh \
    # && /root/server/tools/build_protobuf.sh \
    && export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib \
    && /root/server/tools/make.sh all 
        
CMD ["./restart.sh"]