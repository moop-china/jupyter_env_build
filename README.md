# jupyter_env_build
docker compose 搭建 jupyter单机环境

# file explaination

env.sh指定了各种环境变量，其中：  
* `LOCAL_WORKING_DIR`指定了宿主机的路径，会映射成jupyter的文件根目录
* `PORT`指定了宿主机expose的端口，映射到jupyter的8888端口
* `ACCESS_TOKEN`指定了jupyter的token，如果要生成新的密码，请在有jupyter的python解释器下，执行以下代码来生成密钥。注意，jupyter有自己的生成方法，不同于其他的生成方法。
    ```
    from notebook.auth import passwd
    passwd()
    ```

docker-compose.yml完成了对指定的变量的配置，包括源镜像，volumes映射，ports映射，容器名称，启动命令等，具体写法参照文件内容。

# use guide

首先，切换到jupyter_env_build目录下，在shell中执行`source env.sh`以export环境变量到当前shell，然后执行`docker-compose up`以通过当前目录下的docker-compose.yml创建新的container。

注意，如果要映射宿主机中的目录作为jupyter的文件根目录，请检查权限问题，简单的办法就是`chmod 777 ${dir_path} -R`。
