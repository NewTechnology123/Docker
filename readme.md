## Notes
- Containers & Network Request: [View](https://github.com/NewTechnology123/Docker/issues/8)
- Summary Networking (Cross-)Container Communication: [View](https://github.com/NewTechnology123/Docker/issues/9)
## Description
- Run on nodejs with network to practice **Docker**
## Command
- To build 
    ```
    docker build -t favorites-node .
    ```
- To run 
    ```
    docker run --name favorites -d --rm -p 3000:3000 favorites-node
    ```
- Link working: 
    - Normal (Connect to local and mongoDB Local) 
    ```
    mongodb://127.0.0.1:27017/swfavorites
    ```
    - Internal Docker (Connect to docker and mongoDB Local), special Domain by docker: 
    ```
    mongodb://host.docker.internal:27017/swfavorites
    ``` 
    - All public on Docker have 2 aways:
        1. Connect to docker and mongoDB Docker by IDAddress
            - To build: 
                ```
                Docker run -d --name mongodb mongo
                ```
            - Get struct by command to get **IDAddress** (172.17.0.3)  
                ```
                docker container inspect mongodb
                ``` 
            - Link: 
                ```
                mongodb://172.17.0.3:27017/swfavorites
                ```
        2. Using network  [can read](https://github.com/NewTechnology123/Docker/issues/7)
            - To create network: 
                ```
                docker network create favorites-net
                ```
            - To build: 
                ```
                docker run -d --name mongodb --network favorites-net mongo
                ```
            - Link: 
                ```
                mongodb://172.17.0.3:27017/swfavorites
                ```
            - To run: 
                ```
                docker run --name favorites --network favorites-net -d --rm -p 3000:3000 favorites-node
                 ```
    

