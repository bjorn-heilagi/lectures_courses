# Uso do PostgreSQL no Docker

Siga os passos abaixo para instalar o Docker e utilizar o PostgreSQL via Docker Containers.

## 1. Instalando o Docker

Abaixo segue os passos de instalação do Docker para os sistemas operacionais Windows e Linux.

### 1.1. Windows

Abaixo, segue os passos necessários para instalar o Docker no Windows.

* Acesse o site do [Docker](https://www.docker.com/).
* Efetue o download do **Docker Desktop**.
* Execute o instalador do Docker (Docker Desktop Installer.exe).
* Quando solicitado, selecione o **backend WSL 2** na página de Configuração em vez de Hyper-V. Ou deixe a opção desmarcada para utilizar o Hyper-V. Em sistemas que suportam apenas um backend, o Docker Desktop seleciona automaticamente a opção disponível.
* Siga as instruções no assistente de instalação para autorizar o instalador e prosseguir com a instalação.
* Quando a instalação for concluída com êxito, selecione **Fechar** para finalizar o processo de instalação.
* Inicie o Docker Desktop.

### 1.2. Distribuições Linux derivadas do Ubuntu

* Efetue o download do pacote **.deb** por meio deste [link](https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64&_gl=1*18gfx5f*_gcl_au*NDI0NDA3MDQzLjE3OTQzMjE5MTc.*_ga*MTAxNDE0MzUwMC4xNzk0MzIxOTE3*_ga_XJWPQMJYHQ*czE3OTQzMjE5MTckbzEkZzEkdDE3OTQzMjI1MjUkajUwJGwwJGgw).
* Acesse o terminal (Ctrl + Shift + T).
* No terminal, execute os seguintes passos:
    * Atualize a lista de repositórios para baixar as dependências de que o Docker precisa.
    ```bash
    $ sudo apt-get update
    ```
    * Execute o instalador do Docker (docker-desktop-amd64.deb).
    ```bash
    $ sudo dpkg -i docker-desktop-amd64.deb
    ```
    * Inicie o Docker Desktop.
    ```bash
    $ systemctl --user start docker-desktop
    ```
    * Verifique se o Docker instalou corretamente por meio dos comandos abaixo. Se nenhum deles apresentar uma mensagem de erro, então deu tudo certo na instalação.
    ```bash
    $ docker compose version
    $ docker --version
    $ docker version
    ```

**Observação:** caso apareça um erro informando que você não tem permissão de superusuário, coloque o **sudo** na frente de cada comando do Docker. Ou, ao acessar o terminal, **logue como superusuário** imediatamente.
```bash
sudo su root
```

## 2. PostgreSQL no Docker

A partir de agora, irei considerar que você esteja usando o Powershell do Windows no modo Administrador ou o terminal do Linux logado como superusuário (**root**).

Siga os seguintes passos:

* Verifique se existe algum container do PostgreSQL, se sim, remova-o.
```bash
docker ps -a # lista todos os containers.
docker stop id_container # para a execução do container.
docker rm id_container # remove o container.
```

* Para que seja obtida a versão mais recente do PostgreSQL, remova também a imagem do PostgreSQL, caso ela exista.
```bash
docker rmi id_imagem
```

* Caso exista um volume existente associado ao PostgreSQL, remova-o também.
```bash
docker volume ls # lista todos os volumes criados pelo Docker.
docker volume rm nome_volume # remove um volume.
```

* Baixe a imagem da versão mais recente do PostgreSQL.
```bash
docker pull postgres
```

* Crie e execute o container do PostgreSQL.
```bash
docker run --name curso_bd -e POSTGRES_PASSWORD=curso123 -v pg_curso_bd:/var/lib/postgresql -d -p 5432:5432 postgres
```