# Deploy webshop to localhost

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
