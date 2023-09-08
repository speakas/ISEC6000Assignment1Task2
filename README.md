## Make a copy of the repository
```
git clone https://github.com/speakas/ISEC6000Assignment1Task2.git
```

## How to run it?

1. Go to the cloned directory:
```shell
cd ISEC60000Assignment1Task2/
```
3. Build the application:
```shell
docker compose build
```
4. Apply Django migrations:
```shell
docker compose run --rm api python3 manage.py migrate
```
5. Populate the database with example data and create the admin user:
```shell
docker compose run --rm api python3 manage.py populatedb --createsuperuser
```
*Note that `--createsuperuser` argument creates an admin account for `admin@example.com` with the password set to `admin`.*

6. Run the application:
```shell
docker compose up
```
7. Access the application through your browser
-API
```shell
http://localhost:8000/
```
-Storefront
```shell
http://localhost:3009/
```
-Dashboard
```shell
http://localhost:9003/
```

