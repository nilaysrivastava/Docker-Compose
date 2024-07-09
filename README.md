# MongoDB and Mongo Express Docker Compose Setup

This repository contains a simple Docker Compose configuration to set up MongoDB and Mongo Express. MongoDB is a popular NoSQL database, and Mongo Express is a web-based MongoDB admin interface written in Node.js.

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Docker Compose Configuration

This `docker-compose.yaml` file defines two services: `mongodb` and `mongo-express`. 

```yaml
version: "3"
services:
  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
    volumes:
      - mymongo-data:/data/db
  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - "8081:8081"
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb
volumes:
  mymongo-data:
    driver: local
```

### 3. Running the Services

Navigate to the directory containing the `docker-compose.yaml` file and run the following command:

```bash
docker-compose up -d
```

This command will start the MongoDB and Mongo Express services in detached mode.

### 4. Access Mongo Express

Once the services are running, you can access the Mongo Express web interface by navigating to [http://localhost:8081](http://localhost:8081) in your web browser.

### 5. Stopping the Services

To stop the running services, use the following command:

```bash
docker-compose down
```

This command will stop and remove the containers defined in the `docker-compose.yaml` file.

## Volumes

The `docker-compose.yaml` file uses a Docker volume named `mymongo-data` to persist MongoDB data. This ensures that your MongoDB data is not lost when the container is stopped or removed.

## Environment Variables

The services are configured using environment variables:

- `MONGO_INITDB_ROOT_USERNAME` and `MONGO_INITDB_ROOT_PASSWORD` set the MongoDB admin username and password.
- `ME_CONFIG_MONGODB_ADMINUSERNAME`, `ME_CONFIG_MONGODB_ADMINPASSWORD`, and `ME_CONFIG_MONGODB_SERVER` configure Mongo Express to connect to the MongoDB service.

## Additional Resources

- [MongoDB Documentation](https://docs.mongodb.com/)
- [Mongo Express Documentation](https://github.com/mongo-express/mongo-express)

Feel free to customize the `docker-compose.yaml` file to suit your needs. If you have any questions or run into issues, please open an issue on this repository.
