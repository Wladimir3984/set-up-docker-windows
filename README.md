# set-up-docker-windows
# Instalación de Docker en Linux con WSL2

## Referencias
- [Video tutorial](https://www.youtube.com/watch?v=A34k_dp8CxM&t=646)
- [Documentación para instalar Docker en Linux](https://docs.docker.com/engine/install/ubuntu/)
- [Post instalación](https://docs.docker.com/engine/install/linux-postinstall/)

## Pasos
1. Tener activado WSL, ver en "activar o desactivar las caracteristicas de windows"
2. Instalar Ubuntu desde microsoft store
3. Seguir los pasos de la documentación de Docker para instalar Docker en Linux y la post instalación para no usar sudo:
    1. Actualizar el índice de paquetes apt e instalar los paquetes necesarios para permitir que apt use un repositorio a través de HTTPS:
        ```
        sudo apt-get update
        sudo apt-get install \
            ca-certificates \
            curl \
            gnupg
        ```
    2. Agregar la clave GPG oficial de Docker:
        ```
        sudo mkdir -m 0755 -p /etc/apt/keyrings
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
        ```
    3. Configurar el repositorio:
        ```
        echo \
          "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
          $(lsb_release -cs) stable" | \
          sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        ```
    4. Actualizar el índice de paquetes apt:
        ```
        sudo apt-get update
        ```
    5. Instalar la última versión de Docker:
        ```
        sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
        ```
    6. Verificar que la instalación fue exitosa ejecutando la imagen hello-world:
        ```
        sudo docker run hello-world
        ```
    7. Seguir los pasos de la documentación de post instalación de Docker para evitar el uso de sudo: [Post instalación](https://docs.docker.com/engine/install/linux-postinstall/)
4. Habilitar Docker:
    ```
    sudo systemctl enable docker
    sudo service docker start
    ```
