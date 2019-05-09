## How to use?
## 如何使用？

#### 1. Build the image
#### 1. 构建镜像

###### You can `pull` the image
###### 你可以直接拉取已构建好的镜像

    docker pull registry.cn-hangzhou.aliyuncs.com/xavier/laravel

###### Or You can build it from scratch
###### 或者自己手动构建

    docker build -t xavier/laravel https://raw.githubusercontent.com/FineJadeXavier/docker-laravel/master/Dockerfile

#### <span id="step2Eng">2. Run new container</span>
#### <span id="step2Chn">2. 运行一个新的容器</span>

    docker run -d --name your-laravel -p80:80 -p443:443 xavier/laravel
    
#### 3. Run the `bash` inside the container
#### 3. 进入容器的终端

    docker exec -it your-laravel /bin/bash
    
#### 4. Create new `Laravel` project inside the container
#### 4. 在容器中创建一个新的laravel项目

    rm -rf /var/www  
    cd /var 
    laravel new www
    ## 或者安装指定版本： composer create-project --prefer-dist laravel/laravel blog "5.5.*"
    ## Or install the specified version：  composer create-project --prefer-dist laravel/laravel blog "5.5.*"

#### 5. Create files and associate the appropriate permissions
#### 5. 创建日志目录并给权限

    touch /var/www/storage/logs/laravel.log
    chmod -R 777 /var/www/storage
    
#### 6. Open [localhost](http://localhost/)
#### 6. 打开浏览器访问[http://localhost/](http://localhost/ "Laravel")即可看到运行中的Laravel了

## Other
## 其他问题

### 1. Nginx Config file
### 1. nginx配置文件在哪？

    /etc/nginx/sites-enabled/default.conf

### 2. This error may appear:
### 2. 运行的时候可能会出现:

    Do not run Composer as root/super user! See https://getcomposer.org/root for details

###### This is a warning,just ignore it.
###### 这是一个警告，让我们不要在root用户下使用composer,无视就好

### 3. How to use MySQL and Redis？
### 3. 如何使用MySQL以及Redis？

###### First you need a MySQL/Redis container. In the [second step](#step2Eng), add --link=mysql:your-mysql.
###### 首先你需要一个MySQL/Rediss容器，在[第2步](#step2Chn)的时候加上--link=mysql:your-mysql

    docker run -d --name your-laravel -p80:80 -p443:443 --link=mysql:mysql xavier/laravel
   
###### And the some with Redis
###### Redis 同理

