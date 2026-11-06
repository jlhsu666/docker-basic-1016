# docker-basic-1016

# Network & Volume
sudo docker network create mynet
sudo docker volume create pgdata
sudo docker info pgdata
sudo docker run -d --name mypg --network mynet -e POSTGRES_PASSWORD=secret -v pgdata:/var/lib/postgresql/data postgres:16-alpine
sudo docker run -it --rm --network mynet -e PGPASSWORD=secret postgres:16-alpine psql -h mypg -U postgres -c "CREATE TABLE t(id INT); INSERT INTO t VALUES (42);"
sudo docker rm -f mypg
sudo docker run -d --name mypg2 --network mynet -e POSTGRES_PASSWORD=secret -v pgdata:/var/lib/postgresql/data postgres:16-alpine
sudo docker run -it --rm --network mynet -e PGPASSWORD=secret postgres:16-alpine psql -h mypg2 -U postgres -c "SELECT * FROM t;"
