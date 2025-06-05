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

network
    docker network ls
containers
    docker ps
julia@MT-306729:~/ION-DTN-docker/test$ sudo docker-compose -f test_network.yaml down --volumes
Removing b51b0581c0b1_ion_node1 ... done
Removing 04ea967be537_ion_node2 ... done
Removing network test_ion_net
julia@MT-306729:~/ION-DTN-docker/test$ sudo docker images
REPOSITORY        TAG             IMAGE ID       CREATED          SIZE
ion-image         latest          0ac3b0eb177b   16 minutes ago   869MB
<none>            <none>          27d950e1a9bc   3 hours ago      386MB
<none>            <none>          74567f22bc2c   25 hours ago     869MB
ubuntu            22.04           b103ac8bf22e   5 days ago       77.9MB
gamecat69/ion     latest          1bf0d4061c95   6 days ago       697MB
ion               latest          1bf0d4061c95   6 days ago       697MB
debian            bullseye-slim   06b60f9b8ab4   2 weeks ago      80.7MB
rtmoran/ion-dtn   latest          8ac91a66c46b   3 years ago      136MB
ubuntu            14.04           13b66b487594   4 years ago      197MB
julia@MT-306729:~/ION-DTN-docker/test$ sudo docker-compose -f test_network.yaml up --force-recreate

julia@MT-306729:~/ION-DTN-docker/ion-image$ sudo docker exec -it ion_node1 /bin/bash