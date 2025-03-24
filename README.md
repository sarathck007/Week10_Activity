# Spring Boot Microservices with Load Balancing

This project demonstrates a simple microservices architecture with client-side load balancing using Spring Boot 3.2.3 and Java 21.

## Components

### 1. Eureka Server (RibonUrekaServer)
- Service registry server
- Registers and monitors all microservices
- Default port: 8761

### 2. Backend Service (RibonServer)
- Simple REST service with endpoints
- Registereds with Eureka
- Multiple instances can run on different ports (9090, 9091, 9092)

### 3. Frontend Client (RibonClient)
- Uses Spring Cloud LoadBalancer to distribute requests
- Discovers backend services via Eureka
- Port: 8888

## Setup and Running

1. Build all projects:
   ```
   mvn clean package
   ```

2. Start the Eureka Server:
   ```
   java -jar RibonUrekaServer/target/RibonUrekaServer-0.0.1-SNAPSHOT.jar
   ```

3. Start multiple instances of the Backend Service:
   ```
   java -jar RibonServer/target/RibonServer-0.0.1-SNAPSHOT.jar
   java -jar -Dserver.port=9091 RibonServer/target/RibonServer-0.0.1-SNAPSHOT.jar
   java -jar -Dserver.port=9092 RibonServer/target/RibonServer-0.0.1-SNAPSHOT.jar
   ```

4. Start the Frontend Client:
   ```
   java -jar RibonClient/target/RibbonClient-0.0.1-SNAPSHOT.jar
   ```

## Testing

1. Verify services in Eureka dashboard:
   - Open http://localhost:8761/

2. Test direct access to a backend instance:
   - Open http://localhost:9090/backend

3. Test load balanced access through the client:
   - Open http://localhost:8888/client/frontend
   - Refresh multiple times to see requests distributed to different backend instances


## Technologies

- Java 21
- Spring Boot 3.2.3
- Spring Cloud 2023.0.0
- Spring Cloud LoadBalancer (replacing Netflix Ribbon)
