Getting Started

- [Getting Started](http://localhost/tutorial/)

  ```shell
  docker run -d -p 80:80 docker/getting-started
  ```

  - `-d` - run the container in detached mode (in the background)
  - `-p 80:80` - map port 80 of the host to port 80 in the container
  - `docker/getting-started` - the image to use

  The Docker Dashboard  客户端的界面

  

  What is a container?

  简单来说，是进程。

  这个进程有什么特点， 被你主机上的其他进程进行分离

  

  What is a container image?

  提供隔离的文件系统，包括了依赖，配置，脚本，二进制文件等等。

  环境变量，跑的命令，其他的元数据等等

  

- [Our Application](http://localhost/tutorial/our-application/)

  你 build 了一个MVP-最小可执行的产品

  想要展示如何工作，兼容性-不需要考虑大团队，多名开发者一起的那种场景

  Getting our App

  [Download the ZIP](http://localhost/assets/app.zip)

  解压，之后用VS Code打开

  Build 应用的容器镜像

  创建一个叫做 Dockerfile的文件，文件里面放入以下的内容

  ```html
  FROM node:12-alpine
  # Adding build tools to make yarn install work on Apple silicon / arm64 machines
  RUN apk add --no-cache python2 g++ make
  WORKDIR /app
  COPY . .
  RUN yarn install --production
  CMD ["node", "src/index.js"]
  ```

  之后开始 build

  ```shell
  docker build -t getting-started .
  ```

  

  

  3

  

  

- [Updating our App](http://localhost/tutorial/updating-our-app/)

  1

  

- [Sharing our App](http://localhost/tutorial/sharing-our-app/)

  1

  

- [Persisting our DB](http://localhost/tutorial/persisting-our-data/)

  1

  

- [Using Bind Mounts](http://localhost/tutorial/using-bind-mounts/)

  1

  

- [Multi-Container Apps](http://localhost/tutorial/multi-container-apps/)

  

- [Using Docker Compose](http://localhost/tutorial/using-docker-compose/)

  

- [Image Building Best Practices](http://localhost/tutorial/image-building-best-practices/)

  

- [What Next?](http://localhost/tutorial/what-next/)