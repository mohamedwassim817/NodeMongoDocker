# NodeMongoDocker


create the mongo network to add all the containers in the same network

#docker network create mongo-network

creates the mongoDB container

#docker run -d \
    --p27017: 27017 \
    --net some-network \
    --name some-mongo \
    -e MONGO_INITDB_ROOT_USERNAME = root \
    -e MONGO_INITDB_ROOT_PASSWORD = root \
    mongo

creates the mongo-express container
 
#docker run -d \
    -p8081: 8081 \
    --name mongoexpr \
    --net mongo-network \
    -e ME_CONFIG_MONGODB_ENABLE_ADMIN = "true" \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME = root \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD = root \
    -e ME_CONFIG_BASICAUTH_USERNAME = root \
    -e ME_CONFIG_BASICAUTH_PASSWORD = root \
    -e ME_CONFIG_MONGODB_SERVER = mongow \
    mongo-express: 0.54.0

create a nodejs container where the application will run

#docker run -d -p8081: 80 node --name [container-name]

enter the container if / bin / bash does not work use / bin / sh

#docker exec -it [id_container_node] / bin / bash

check that git is installed

#git --version

clone the repo inside the container

#git clone https://gitlab.com/nanuchi/techworld-js-docker-demo-app.git

go to the ./app/server.js file and modify in the code the connection to mongoDB according to the container ip
mongo in your network you will modify the ./app/server.js file in the host and copy it to the container
because there is no editor in the container

    
    1- in the host terminal

     #docker inspect [network_name]

  
    2- take the address of the container and modify it in the file in ./app/server.js the clause
    
     [// use when starting application locally]
     [let mongoUrlLocal = "mongodb: // admin: password @ localhost: 27017";]


    3- delete the ./app/server.js file in the container
     
     #rm -r server.js
     
     4- with docker cp copy the file from the host to the container

     #docker cp [non_du_fichier] [container id]: [directory in the container]

     
     5- return to the interior of the container
   
 #npm install
    
 #node server.js

And the app running, consult the application and add the name of the database which is in server.js and the collection in mango-express
http: // localhost: 8081
http: // localhost: 3000
