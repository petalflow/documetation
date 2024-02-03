O projeto consiste em três aplicações que operam em conjunto, embora inicialmente se apresentem como entidades separadas. A API desempenha o papel de ferramenta responsável pelo controle, gerenciamento e persistência dos dados. Associado a ela está o servidor, responsável por executar as ações que são obtidas por meio da API e armazenadas em um banco de dados. Neste projeto, optamos por utilizar o MongoDB devido à necessidade de lidar com grandes volumes de dados, como logs, scripts de execução em Python e SQL. Estamos considerando a inclusão de outra linguagem de captura em breve.

# 
    petalsync/
        logs/
        config/
        app.py
        service.py  # Application execution configuration file.
    Dockerfile
    docker-compose.yml
    project.toml
    supervisor.conf
    README.md
        ...

Por fim, temos a aplicação gráfica, que contribui para uma experiência mais amigável do Petalsync. Essa interface está sendo desenvolvida em React e, embora atualmente não faça parte do pacote Petalsync, os usuários têm a opção de baixá-la e adicioná-la à mesma árvore de diretórios, conforme exemplificado acima.