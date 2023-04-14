## Notes
- Docker Compose Elegant Multi-Container Orchestration: [read](https://github.com/NewTechnology123/Docker/issues/12)
- Docker Compose Key Commands: [read](https://github.com/NewTechnology123/Docker/issues/13)
- localhost => 127.0.0.1
- Docker-compose name:
    - Image default: "folder-SerivceName"
        - Change it by: `image`: Name
    - Container default: "ServiceName-1"
        - Change it by: `container_name`: Name
        
- Docker-compose: 
    - Don't need using `network` for containers. Docker will automatically create a new environment and add for all the services specified in this compose file.
        - Notes: In the case you add 1 services which **network** you want. Then it not just be added to the default network
    - Any **named volumes** you're using in your services **have** to be listed here in this case **data**. (**Strange** but this is the syntax Docker wants) for being aware of named volumes. It should create for your services
        - If you then use the same volume name in different services. The volume will be shared so different containers (the same forlder on your hosting machine)
        - **Anonymous volumes** and **bind mounts** don't need to specified here.

- Build in docker-compose:
    - Case 1:
        - ```build: ./backend```
    - Case 2:
        - ```
          build: 
            context: ./backend
            dockerfile: Dockerfile
            args:
             - some-args: 1
        ```
    > Using **case 2** when you want set custom other folder, name Dockerfile or set variables *arguments*.
- Child on **service**:
    - `stdin_open: true`: = `-i` That this service needs an open input connection
    - `tty: true`: = `-t`  Show result output on terminal
    - Notes: You can read more command docker [here](https://github.com/NewTechnology123/Docker/issues/3)   
   

## Description
- Build step: mongo, frontend and backend. After run `docker-compose up`

## Command
- Command convert to docker-compose.yaml:
    - MongoDB: `docker run --name mongodb --rm -d -v data:/data/db --network goals-net mongo `
    - Nodejs: `docker run --name goals-backend -v D:/learn_docker/backend:/app -v logs:/app/logs -v /app/node_modules --rm -d --network goals-net -p 80:80 goals-node` 
    - Reactjs: `docker run -v D:/learn_docker/frontend/src:/app/src --name goals-frontend --rm -p:3000:3000 -d -it goals-react`

