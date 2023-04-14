## Notes
- Read: [Theory volumn](https://github.com/NewTechnology123/Docker/issues/4)
- Summary: [Image & Volume Summary](https://github.com/NewTechnology123/Docker/issues/6)


## Description
- Run on nodejs to practice **Docker**
## Command
> 1. Building & Understanding the Demo App 
- To build `docker build -t feedback-node .`
- To run with port 3000 at local, name: feedback-app and auto remove container when it stop `docker run -p 3000:80 -d --name feedback-app --rm feedback-node`
    - It will create file {title}.txt and description on that file. You can check it on http://localhost:3000/feedback/{title}.txt

> 2. Combining & Merging Different Volumes
- To build 
    ```
    docker build -t feedback-node:volumes .
    ```
- To run is replace current volumn (Remove line Volumn in **Dockerfile**)
    ```
    docker run -p 3000:80 -d --name feedback-app --rm feedback-node:volumes
    ```
- To run container, it not overrite if it exits you can try: 
    ```
    docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback --rm feedback-node:volumes`
    ```
- Command: 
    ```
    docker run -p 3000:80 -d --rm --name feedback-app -v feedback:/app/feedback -v "D:/learn_docker:/app:ro" -v /app/node_modules --rm feedback-node:volumes
    ``` 
    - `-v feedback:/app/feedback`: This option creates a named volume named "feedback" and mounts it to the directory /app/feedback inside the container
    - `-v "D:/learn_docker:/app"`: This option mounts the host directory D:/learn_docker to the directory /app inside the container
    - `:ro`: Is setup volume is read only. Setup local to avoid override
    - `-v /app/node_modules`: This option mounts an **anonymous volume** to the directory /app/node_modules inside the container (In the case, this command is not exits then error. Vì "RUN NPM INSTALL" sẽ tải xuống trong `/app/node_modules` của Docker container. Khi gắn `-v` để kết nối giữa host và container thì các thư mục trong container sẽ được ghi đè bởi các thư muc trên host. Nên nếu không có  -v /app/node_modules, thư mục /app/node_modules trong container sẽ bị ghi đè bởi thư mục trên host và các phụ thuộc đã được cài đặt sẽ bị xóa. (Nếu đã tồn tại thì host rồi bỏ qua) ) 
> 3. Nodemon
- Nodemon: To view log for docker is better, realtime.
- Volumes & Bind Mounts: [read](https://github.com/NewTechnology123/Docker/issues/5)
> 4. .dockerignore
- Help part copy is skip this file/forder
> 5. Arguments and environtment [read](https://github.com/NewTechnology123/Docker/issues/14)



