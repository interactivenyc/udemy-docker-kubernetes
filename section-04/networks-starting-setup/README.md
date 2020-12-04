docker network create favorites-net
docker run -d --name mongodb --network favorites-net -p 27017:27017 mongo

docker build -t favorites-node .
docker run --name favorites --network favorites-net -d --rm -p 3000:3000 favorites-node 

Test this with these Postman commands

GET localhost:3000/favorites (initially empty)
GET localdochost:3000/people (fetches people from swapi)
POST localhost:3000/favorites with this body:

    {
        "name" : "Luke Skywalker",
        "type" : "character",
        "url" : "http://swapi.dev/api/planets/1/"
    }

GET localhost:3000/favorites (shows stored favorite) 