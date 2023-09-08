## Make a copy of the repository
```
git clone https://github.com/speakas/ISEC6000Assignment1Task2.git
```

## How to run it?

1. Go to the cloned directory:
```shell
cd ISEC60000Assignment1Task2/
```
2. Build the application:
```shell
docker compose build
```
3. Apply Django migrations:
```shell
docker compose run --rm api python3 manage.py migrate
```
4. Populate the database with example data and create the admin user:
```shell
docker compose run --rm api python3 manage.py populatedb --createsuperuser
```
*Note that `--createsuperuser` argument creates an admin account for `admin@example.com` with the password set to `admin`.*

5. Run the application:
```shell
docker compose up
```
6. Access the application through your browser

- API
```shell
http://localhost:8000/
```
- Storefront
```shell
http://localhost:3009/
```
- Dashboard
```shell
http://localhost:9003/
```


## Steps needed to setup docker-compose.yaml
The compose file needs to be setup to allow the storefront to run alongside the api. To do this, the storefront docker-compose.yaml file can be copied into the saleor-platform docker-compose.yaml file with a few updates.

The build needs to be fed the path to the react-storefront location. eg ./react-storefront

## Configuring the API Address for Docker Containers

When setting up Docker containers for the Saleor platform, it's crucial to correctly configure the API address. Ensure you update the API reference from `http://localhost:8000/graphql` to `http://api:8000/graphql`. This change is essential because each docker image resides in its unique container. To communicate, they reference each other using their respective image names as the address.

### Ensuring Docker Containers Are on the Same Network

All involved Docker containers must be on the same network to communicate seamlessly. This needs to be added to the networks list for each image on the docker-compose.yaml file. To verify this:

1. Enter the target Docker container using the `docker exec` command:
```bash
docker exec -it react-storefront bash
```
Inside the container, use the curl command to check the connectivity:

```bash
curl http://api:8000
```
If successful, this means the containers can communicate with each other, ensuring smooth operation.
