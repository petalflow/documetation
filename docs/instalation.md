# Instalação

A instalação do PetalSync é bastante simples e pode ser realizada em servidores Linux e Windows através do Docker.

## Configurando o Projeto Localmente

Para executar o projeto, siga os passos abaixo:

1. Clone o [repositório](https://github.com/petalflow/petalsync) do projeto no Github.
2. Instale as dependências utilizando o gerenciador de pacotes `Poetry` com o comando:

    ```
poetry install
    ```

3. A API de integração é construída sobre o FastAPI 0.95.1 e requer o Python na versão superior a 3.10. Qualquer adaptação necessária pode ser feita em versões subsequentes.
4. Crie um arquivo `.env` contendo a string de conexão com o MongoDB. Veja o exemplo abaixo do local de criação e do conteúdo do arquivo:

```
    petalsync/
        api/
        app/
        ...
        .env  # Conteúdo do arquivo contendo a string de conexão com o banco de dados
```

    Exemplo do conteúdo do arquivo:

    ```
    MONGODB_CONNECTION_STRING=mongodb://user:password@localhost:27017/?authMechanism=DEFAULT
    MONGODB_CONNECTION_STRING_DB=database
    ```

5. Execute o servidor web com o comando:

    ```
    uvicorn app:app --reload
    ```

## Instalação Local via Docker

Para a instalação via Docker, é necessário possuir o Docker [instalado](https://docs.docker.com/engine/install/ubuntu/).

Configure o arquivo `docker-compose.yml` para adequar as configurações ao seu ambiente. Esta implementação do projeto para a imagem Docker está em desenvolvimento, portanto, avalie a viabilidade das configurações fornecidas.

```yaml
version: '3'

services:
  petalsync:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8000:8000"
      - "5000:5000"
    networks:
      - hostnet
    environment:
      MONGO_HOST: host.docker.internal
networks:
  hostnet:
    external: true


```

Optamos por utilizar o Supervisor para monitoramento e controle dos nossos processos. Tanto a API como Processo de ETL será monitorados pelo Supervisor. Toda a configuração será passada para o controle do Supervidor através do arquivo supervisord.conf.


```bash
[program:etl]
command=/opt/venv/bin/python /petalsync/etl.py
directory=/petalsync
autostart=true
autorestart=true
startretries=3
redirect_stderr=true
stdout_logfile=/petalsync/logs/etl/etl.log
stdout_logfile_maxbytes=10MB

``` 

Com o projeto devidamente baixado em sua máquina, para seguir com a criação da projeton em um container docker, basta executar os comando baixo:

Use o comando abaixo para inicar o seu container. A necesside do comando linux sudo depende da configuraçlao do seu amviente local. 

```
sudo docker-compose up -d
```


As aplicação executa por padrão na porta 8000. Você pode conferir em seu navegador através do `127.0.0.1:8000/docs`.







