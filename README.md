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
1. Crear i edita `Dockerfile`
2. Crear imatge 
    ```bash
    sudo docker build -t ion-image .
    ```
3. Run 
    ```bash
    sudo docker run -d -p 80:80 ion-image:latest
    ```