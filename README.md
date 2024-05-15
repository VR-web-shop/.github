# Deploy webshop to localhost
NOTE: It requires a GitHub (Classic) access token with package read access to install packages from the organization NPM Registry.

## Setup Auth
```
# Clone repo
git clone https://github.com/VR-web-shop/Auth.git

# Change directory
cd Auth

# Copy config files
# NOTE: these must be configured manual the first time.
cp .env.example cp.env

# Setup DB
npm run migrate
npm run seed

docker build -t auth:v1.0 .
docker run -p 3000:3000 auth:v1.0
```

## Setup Products
```
# Clone repo
git clone https://github.com/VR-web-shop/Products.git

# Change directory
cd Products

# Copy config files
# NOTE: these must be configured manual the first time.
# NOTE: NPM Registry require organization access.
cp .env.example cp.env
cp .npmrc.example cp.npmrc

# Setup DB
npm run migrate
npm run seed

docker build -t products:v1.0 .
docker run -p 3002:3002 products:v1.0
```

## Setup Scenes
```
# Clone repo
git clone https://github.com/VR-web-shop/Scenes.git

# Change directory
cd Scenes

# Copy config files
# NOTE: NPM Registry require organization access.
# NOTE: these must be configured manual the first time.
cp .env.example cp.env
cp .npmrc.example cp.npmrc

# Setup DB
npm run migrate
npm run seed

docker build -t scenes:v1.0 .
docker run -p 3003:3003 scenes:v1.0
```

## Setup Shopping Cart
```
# Clone repo
git clone https://github.com/VR-web-shop/Shopping-Cart.git

# Change directory
cd Shopping-Cart

# Copy config files
# NOTE: these must be configured manual the first time.
# NOTE: NPM Registry require organization access.
cp .env.example cp.env
cp .npmrc.example cp.npmrc

# Setup DB
npm run migrate
npm run seed

docker build -t shopping-cart:v1.0 .
docker run -p 3004:3004 shopping-cart:v1.0
```

## Setup Admin Client
```
# Clone repo
git clone https://github.com/VR-web-shop/Admin-Client

# Change directory
cd Admin-Client

# Copy config files
# NOTE: these must be configured manual the first time.
# NOTE: NPM Registry require organization access.
cp .env.example cp.env
cp .npmrc.example cp.npmrc

docker build -t adminclient:v1.0 .
docker run -p 5173:5173 adminclient:v1.0
```

## Setup Scenes VR Client
```
# Clone repo
git clone https://github.com/VR-web-shop/Scenes-Editor-Client

# Change directory
cd Scenes-Editor-Client

# Copy config files
# NOTE: these must be configured manual the first time.
# NOTE: NPM Registry require organization access.
cp .env.example cp.env
cp .npmrc.example cp.npmrc

docker build -t sceneseditorclient:v1.0 .
docker run -p 5174:5174 sceneseditorclient:v1.0
```

## Setup Scenes Editor Client
```
# Clone repo
git clone https://github.com/VR-web-shop/Scenes-VR-Client

# Change directory
cd Scenes-VR-Client

# Copy config files
# NOTE: these must be configured manual the first time.
# NOTE: NPM Registry require organization access.
cp .env.example cp.env
cp .npmrc.example cp.npmrc

docker build -t scenesvrclient:v1.0 .
docker run -p 5175:5175 scenesvrclient:v1.0
```

## Setup MySQL & RabbitMQ & Elasticsearch & Kibana
```
mkdir other-services
cd other-services

cat <<EOF > docker-compose.yaml
services:
  mysql:
    image: mysql
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_DATABASE=db
    ports:
      - "3306:3306"
    volumes:
      - mysql-volume:/var/lib/mysql

  rabbit:
    image: rabbitmq:latest
    environment:
      - RABBITMQ_DEFAULT_USER=rabbit
      - RABBITMQ_DEFAULT_PASS=password
    ports:
      - "5672:5672"
      - "15672:15672"

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.13.4
    ulimits:
      memlock:
        soft: -1
        hard: -1
    ports:
      - 9200:9200

  kibana:
    image: docker.elastic.co/kibana/kibana:8.13.4
    ports:
      - 5601:5601
    depends_on:
      - elasticsearch
    environment:
      ELASTICSEARCH_URL: http://elasticsearch:9200
      ELASTICSEARCH_HOSTS: http://elasticsearch:9200
      ELASTICSEARCH_USERNAME: kibana_system

volumes:
  mysql-volume:
EOF

docker compose up
```
