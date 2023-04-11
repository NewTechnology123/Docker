## Description
- Run on nodejs to practice **Docker**
## Command
> 1. Building & Understanding the Demo App 
- To build `docker build -t feedback-node .`
- To run with port 3000 at local, name: feedback-app and auto remove container when it stop `docker run -p 3000:80 -d --name feedback-app --rm feedback-node`
    - It will create file {title}.txt and description on that file. You can check it on http://localhost:3000/feedback/{title}.txt
