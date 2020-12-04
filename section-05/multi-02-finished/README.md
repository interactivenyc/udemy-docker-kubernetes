# create shared docker network
docker network create goals-net

# run mongodb container - stock from docker hub
docker run -d --name mongodb --network goals-net --rm -p 27017:27017 -v /Users/stevewarren/Projects/Udemy/udemy-docker-kubernetes/section-05/multi-02-finished/backend/data:/data/db -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=secret mongo 

# THIS IS THE UNMODIFIED VERSION
    docker run -d --name mongodb --network goals-net --rm -v data:/data/db -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=secret mongo 


# build backend image
docker build -t goals-node .

# run backend container
docker run --name goals-backend --network goals-net --rm -p 80:80 goals-node 

# build frontend image
docker build -t goals-react .

# run frontend container
docker run --name goals-frontend --network goals-net -d -it --rm -p 3000:3000 -v /Users/stevewarren/Projects/Udemy/udemy-docker-kubernetes/section-05/multi-02-finished/frontend/src:/app/src goals-react 

