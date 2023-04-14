## Notes
- Building Multi-Container Applications with Docker: [read](https://github.com/NewTechnology123/Docker/issues/10)
- localhost => 127.0.0.1
- Docker network command: [view](https://github.com/NewTechnology123/Docker/issues/11)
## Description
- Building Multi-Container Applications with Docker
- Detail:
    - Challenge 1: Run local mongoDB + nodejs + reactjs.
        ```
        mongodb://127.0.0.1:27017/course-goals
        ```
    - Challenge 2: Run container nodejs + mongoDB local 
        ```
        mongodb://host.docker.internal:27017/course-goals
        ```
    - Challenge 3: Connect from **Challenge 2** to reactjs (through port command)
    - Challenge 4: Connect from Nodejs Docker to MongoDB Docker. (View **all** below. Create a network **goals-net**, public and run it.)
        ```
        mongodb://mongodb:27017/course-goals
        ```

## Command
- To build and start mongoDB (This step need get **IDAddress** of mongoDB by logs and share port)
    ```
    docker run --name mongodb --rm -d -p 27017:27017 mongo
    ```
- Backend:
    - Build image: 
        ```
        docker build -t goals-node .
        ```
    - Build container (It's okey. But it not yet connect **frontend** local ). You can try below: 
        ```
        docker run --name goals-backend --rm goals-node`
        ```   
    - (`-p` This allows access the container's services (e.g., a web server) using your web browser or another client. Expose the relevant port(s) to the host machine.) -> Connect (Container nodejs) to reactjs
        ```
        docker run --name goals-backend --rm -d -p 80:80 goals-node
        ```
- Front-end:
    - Build image: 
    ```
    docker build -t goals-react .
    ```
    - Build container (Need `-it` to feed warning input can need (logic of react))
    ```
    docker run --name goals-frontend --rm -p:3000:3000 -d -it goals-react
    ```   
- All:
    - Create network goals-net: 
        ```
        docker network create goals-net
        ```
    - Public network of mongodb: 
        ```
        docker run --name mongodb --rm -d --network goals-net mongo
        ```
    - In backend is nodejs connect to network: 
        ```
        docker run --name goals-backend --rm -d --network goals-net goals-node
        ```
    - Frontend need change from **localhost** to **goals-backend** and must build image again (command need add tag network of mongoDB)  
        ```
        docker run --name goals-frontend --rm -p:3000:3000 --network goals-net -d -it goals-react
        ```
    - Bug (can't connect reactjs to nodejs): It's true logic. But path myseft has no idea and goals backend should be. Related to reactjs. So to commication between to our local machine. Change **goals-backend** to **localhost**
    - Rebuild and try again:
        - Frontend command run no need tag network.
        - Backend need share port 
            ```
            docker run --name goals-backend --rm -d --network goals-net -p 80:80 goals-node
            ```
- Adding Data Persistence to MongoDB with Volumes (By name because when mongoDB stop data will be clear)
    - MongoDB: 
        ```
        docker run --name mongodb --rm -d -v data:/data/db --network goals-net mongo 
        ```
    - Nodejs: 
        ```
        docker run --name goals-backend -v D:/learn_docker/backend:/app -v logs:/app/logs -v /app/node_modules --rm -d --network goals-net -p 80:80 goals-node
        ```
    - Reactjs: 
        ```
        docker run -v D:/learn_docker/frontend/src:/app/src --name goals-frontend --rm -p:3000:3000 -d -it goals-react
        ```
- Authenication:
    - Read [SetAuthenication MongoDB](https://hub.docker.com/_/mongo)
    - Login [MongoDB](https://www.mongodb.com/docs/manual/reference/connection-string/)
        ```
        mongodb://max:secret@mongodb:27017/course-goals?authSource=admin&authMechanism=SCRAM-SHA-256
        ```
    - Command:
        ```
        docker run --name mongodb --rm -d -v data:/data/db --network goals-net -e MONGO_INITDB_ROOT_USERNAME=max -e MONGO_INITDB_ROOT_PASSWORD=secret mongo 
        ```

