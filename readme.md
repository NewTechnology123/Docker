## Notes
- Containers & Network Request: [View](https://github.com/NewTechnology123/Docker/issues/8)
## Description
- Run on nodejs with network to practice **Docker**
## Command
- To build ```docker build -t favorites-node .```
- To run ```docker run --name favorites -d --rm -p 3000:3000 favorites-node```
- Link working: 
    - Normal (Connect to local and mongoDB Local): ```mongodb://127.0.0.1:27017/swfavorites```
    - Internal Docker (Connect to docker and mongoDB Local): ```mongodb://host.docker.internal:27017/swfavorites``` (special Domain by docker, no volume)
    - All on Docker (Connect to docker anhd mongoDB Docker by IDAddress):
        - To build: ```Docker run -d --name mongodb mongo```
        - Get struct by command ```docker container inspect mongodb``` and find to **IDAddress** and get it (172.17.0.3) 
        - Link: ```mongodb://172.17.0.3:27017/swfavorites```

- Creating container networks (standard => share all container): [read](https://github.com/NewTechnology123/Docker/issues/7)
    - To create network: ```docker network create favorites-net```
    - To build: ```docker run -d --name mongodb --network favorites-net mongo```
    - Link: ```mongodb://172.17.0.3:27017/swfavorites```
    - To run: ```docker run --name favorites --network favorites-net -d --rm -p 3000:3000 favorites-node```
    

đính kèm thêm hình ảnh
