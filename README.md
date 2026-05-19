services:
  mongo:
    image: mongo:8.0
    container_name: mongodb
    restart: always
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: admin123
    volumes:
      - mongo_data:/data/db

  nodeapp:
    build: .
    container_name: node_mongodb
    restart: always
    ports:
      - "3000:3000"
    environment:
      MONGO_URL: mongodb://admin:admin123@mongo:27017/mvcdb?authSource=admin
    depends_on:
      - mongo

volumes:
  mongo_data:
