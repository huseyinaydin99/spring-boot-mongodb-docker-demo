# springboot-mongodb-docker - Türkçe - English
Deploying Spring Boot and MongoDB as Containers Using Docker and Docker Compose --
### Docker Compose kullanarak Spring Boot uygulamasını Deploy et ve mongo db uygulamasını yayına al.! 

**Steps & Commands - Adımlar ve Komutlar**

- [x] pull mongo image from docker hub(docker hub'dan mongo imajını çek / indir) **`docker pull mongo:latest`**
- [x] run mongo image(mongo imajını çalıştır) **`docker run -d -p 27017:27017 --name huseyinaydinmongodb mongo:latest`**
- [x] dockerize spring boot application (Spring Boot uygulamasını dockerlaştır) **`docker build -t springboot-mongodb:1.0 .`**
- [x] run spring boot docker image and link that container to mongo container 
   **`docker run -p 8080:8080 --name springboot-mongodb --link huseyinaydinmongodb:mongo -d springboot-mongodb:1.0`**
- [x] check docker running containers(docker üzerinde çalışan konteynırları ve prosesleri kontrol et)  **`docker ps`** it should display two container ids / ID'lere göre görüntülenecektir.!
- [x] check logs of spring boot image(Spring Boot imajının loglarını kontrol et ve listele) **`docker logs springboot-mongodb`**
- [x] if all good access your api / her şey yolundaysa API'a erişelim.
```bash script'i : ->
curl --location --request POST 'http://localhost:8080/books' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id":1,
    "bookName":"corejava",
    "authorName":"Basant"
}'
```
- [x] login to mongo terminal to verify records(mongo db'nin kayıtlarına ulaşmak için login(kimlik doğrulaması yapalım)) **`docker exec -it huseyinaydinmongodb bash`**
- type mongo and enter
- show dbs
- use book
- show collections
- db.book.find().pretty()

**Use Docker Compose - Docker Compose Kullanımı**

- [x] Kill running container / Bütün çalışan containerleri durdur / öldür:
```
docker rm <containerId>
```

#### docker-compose.yml - file / dosyası

```yaml
version: "3"
services:
  huseyinaydinmongodb:
    image: mongo:latest
    container_name: "huseyinaydinmongodb"
    ports:
      - 27017:27017
  springboot-mongodb:
    image: springboot-mongodb:1.0
    container_name: springboot-mongodb
    ports:
      - 8080:8080
    links:
      - huseyinaydinmongodb
```
- [x] navigate to resources folder:
```
springboot-mongo-docker/src/main/resources and run docker-compose up
springboot-mongo-docker/src/main/resources ve çalıştır docker-compose up komutunu
```
