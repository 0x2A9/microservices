# Microservices
Minimal example of microservices with infrastructure for learning and experimentation

# Set Up with Kubernetes
- `kubectl`, `make` and `minikube` should already be installed
- Make sure the `docker daemon`, `minikube` are running and `ingress`, `ingress-dns` addons are available. If not, then start and enable them with:
	```bash
	sudo systemctl start docker
	minikube start
	minikube addons enable ingress
	minikube addons enable ingress-dns
	```
- `80` port of the host machine should not be in use
- Add hosts to the `/etc/hosts`:
	```bash
	127.0.0.1       ui
	127.0.0.1       gateway
	```
- Run the following command from the **project root**:
	```bash
	make k8s_start
	```
- The app will be available under the:
	```bash
	http://ui
	http://gateway
	```

# Set Up with Docker
- `docker engine`, `docker compose` and `make` should already be installed, `docker engine` should run
- `8080` and `8888` ports of the host machine should not be in use
- Create `.env` file using `.env.dist` as template
- Run the following command from the **project root**:
	```bash
	make docker_start
	```
- To stop containers run the following command from the **project root**:
	```bash
	make docker_stop
	```
- The app will be available under the following origins:
	```bash
	http://localhost:8080 - ui
	http://localhost:8888 - gateway
	```

# Set Up Manually
- `docker engine`, `docker compose` should already be installed, `docker engine` should run
- Required: 
	- `make 4.3`;
	- `nodejs 18.16.1`;
	- `protoc 3.21.12`;
	- `go 1.21.3`;
	- `golang-migrate 4.16.2`;
	- `sqlc 1.24.0`;
- `8080`, `8888`, `50051`, `9090`, `5432` ports of the host machine should not be in use
- During the initial setup (first run) execute the following command from the **project root**:
	```bash
	make dev_env_setup
	```
- To run the project with all microservices:
	```bash
	make dev_env_up
	```
- If it is the first run and the DB is empty: 
	```bash
	make db_setup
	```
- The app will be available under the following origins:
	```bash
	http://localhost:8080  - ui
	http://localhost:8888  - gateway HTTP
	localhost:50051        - gateway gRPC
	localhost:9090         - auth gRPC
	```