# opensesame

Simple authentication service and permission management.

Check out [opensasme-back](https://github.com/macolmenerori/opensesame-back) for the API, and [opensesame-front](https://github.com/macolmenerori/opensesame-front) for the front part, with a simple and beautiful interface to interact with this service. More information on how the API and the front part works on their respective repos.

## Requirements

- [Docker](https://www.docker.com/products/docker-desktop/)
- [docker-compose](https://docs.docker.com/compose/install/)

## How to set up and run the full project

1. Clone this repo

```
git clone https://github.com/macolmenerori/opensesame
```

2. Start the service

```
docker-compose up -d
```

3. Everything is ready now, go to `http://localhost:80` and sign in with default email and password

```
email: admin@admin.com
password: administrator
```

## How to set up and run individual parts of the project

First of all, clone this repo

```
git clone https://github.com/macolmenerori/opensesame
```

### Database

1. Build

```
docker build -t opensesame-db .
```

2. Run

```
docker run -d \
  --name opensesame-db \
  -p 27017:27017 \
  opensesame-db
```

### opensesame-back

```
docker build -t opensesame-back ./opensesame-back
```

2. Run

```
docker run -d \
  --name opensesame-back \
  -e NODE_ENV=production \
  -e PORT=8080 \
  -e DB_NAME=opensesame \
  -e DATABASE= \
  -e PASSWORD_HASH_DIFFICULTY=12 \
  -e JWT_SECRET=jc2TNsWyaM3DdKkhurJL8QGzCvX9BfUY \
  -e JWT_EXPIRES_IN=7d
  -e JWT_COOKIE_EXPIRES_IN=7
  -e RATELIMIT_MAXCONNECTIONS=100
  -e RATELIMIT_WINDOWMS=3600000
  -e CORS_WHITELIST=http://localhost:3000
  -p 8080:8080 \
  opensesame-back
```

### opensesame-front

```
docker build -t opensesame-front ./opensesame-front
```

2. Run

```
docker run -d \
  --name opensesame-front \
  -e NODE_ENV=development \
  -e BASE_URL_API=http://localhost:8080/api \
  -p 3000:3000 \
  opensesame-front
```
