# Dockerfile简介
- 构建镜像的方式有两种：一种是基于容器制作，另一种就是通过Dockerfile。Dockerfile其实就是我们用来构建Docker镜像的源码，当然这不是所谓的编程源码，而是一些命令的组合，只要理解它的逻辑和语法格式，就可以编写Dockerfile了。

# Dockerfile规范
- Dockerfile整体就两类语句组成：
`# Comment` 注释信息
`Instruction arguments` 指令 参数，一行一个指令。

- Dockerfile文件名首字母必须大写。
- Dockerfile指令不区分大小写，但是为方便和参数做区分，通常指令使用大写字母。
- Dockerfile中指令按顺序从上至下依次执行。
- Dockerfile中第一个非注释行必须是FROM指令，用来指定制作当前镜像依据的是哪个基础镜像。
- Dockerfile中需要调用的文件必须跟Dockerfile文件在同一目录下，或者在其子目录下，父目录或者其它路径无效`

# Dockerfile常用指令
- From指令：指定继承哪个镜像
- ADD : 将工作目录下的某个目录或者文件copy到镜像的某个路径下
- Run：执行shell 命令
- ENTRYPOINT: 指定容器启动脚本
- ENV：指定容器启动时的环境变量(注意，只有在容器启动时，启动脚本能读取到，如果希望其他用户登录到容器也生效的话，需要写入.bashrc)
- USER：容器启动时使用的用户
- WORKDIR: 容器启动时的工作目录

# Dockerfile执行
- 通过FROM指令使用基础镜像启动一个临时容器 FROM
- 在临时容器中根据dockerfile中的指令安装软件或其他改变 RUN ADD ENV COMMIIT
- 使用docker commit 命令 将临时容器 commiit成一个新的镜像收尾
- 删除临时容器，给新镜像用docker tag命令起名字

# 制作镜像命令
  `docker build -t 镜像名称:tag [工作目录]`

# 示例
自制jenkins容器
```
#从tomcat的镜像开始创建
FROM jenkins:latest
USER root
#声明作者
MAINTAINER tester "gonxc"
ARG JENKINS_HOME=/var/jenkins_home
ARG REF=/usr/share/jenkins/ref
#清理docker镜像中已有的内容
#RUN chmod 755 /usr/share/jenkins/jenkins.war
RUN rm -f /usr/share/jenkins/jenkins.war
#RUN mkdir /usr
#下载新的jenkins.war
USER jenkins
RUN cd /usr/share/jenkins/
ADD jenkins.war .
#对外暴露8080端口
EXPOSE 8080 50000
#执行启动jenkins命令
#CMD ["java", "-Dfile.encoding=UTF8 -Duser.timezone=GMT+08", "-jar", "jenkins.war"]
#CMD ["java", "-jar", "jenkins.war", "-Dfile.encoding=UTF8 -Duser.timezone=GMT+08"]
CMD ["export"]
```
自制基于tomcat的镜像
```
#从tomcat的镜像开始创建
FROM tomcat:latest
#声明作者
MAINTAINER tester "gongxc"
#清理docker镜像中已有的内容
RUN rm -rf /usr/local/tomcat/webapps/ROOT
RUN rm -f /usr/local/tomcat/webapps/ROOT.war
#将新的ROOT.war 复制到镜像中的指定位置
ADD target/ROOT.war /usr/local/tomcat/webapps
#对外暴露8080端口
EXPOSE 8080
#等于执行 catalina.sh run
CMD ["/usr/local/tomcat/bin/catalina.sh","run"]
```
