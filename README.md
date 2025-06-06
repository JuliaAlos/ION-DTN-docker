# ION-DTN-docker
Docker image and set up to test ION-DTN software


## Recompilar ION-DTN Repo
1. Edita el `Makefile.am`

    * Afegeix les instruccions per compoilar el nou fitxer.

    * Afegir intruccions a `bpv6/doc/pod1/<file_name>.pod` i `bpv7/doc/pod1/<file_name>.pod`

2. Regenera el `Makefile`
    ```bash
    aclocal
    autoconf
    automake --add-missing
    ```
3. Neteja, compila i install
    ```bahs
	make clean
	./configure
	make
	sudo make install
    ```

## Com crear DOCKER IMAGE
1. Crear i edita `Dockerfile` en la carpeta `ion-image/`
2. Crear imatge 
    ```bash
    sudo docker build -t ion-image .
    ```
3. Corre imatge (Per comprobar correcte instalacio)
    ```bash
    sudo docker run -d ion-image:latest
    ```
4. Imatges creades
    ```bash
    sudo docker images
    sudo docker rmi -f 0e6dc06dfff3
    ```
5. Accedir terminal imatge
    ```bash
    sudo docker run -it ion-image:latest /bin/bash
    ```

## Run Nodes test
1. Navega a la carpeta `ION-DTN-docker/test/`
    ```bash
    sudo docker-compose -f test_network.yaml up
    ```

## Extra
1. View networks
    ```bash
    docker network ls
    ```
2. View containers
    ```bash
    docker ps
    ```
3. View images
    ```bash
    sudo docker images
    sudo docker rmi -f <Image ID> # To delete old image
    ```
4. Down volumes
    ```bash
    sudo docker-compose -f test_network.yaml down --volumes
    ```
5. Force recompilation
    ```bash
    sudo docker-compose -f test_network.yaml up --force-recreate
    ```
6. Connect to one volume
    ```bash
    sudo docker exec -it ion_node1 /bin/bash
    ```