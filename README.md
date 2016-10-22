# Docker-Compose wordpress
Cria uma maquina Wordpress utilizando Docker,
e persiste os dados dentro de um diretório pré-configurado no ficheiro docker-compose.yml

## Instalação
1. Atualize a lista de pacotes:
`sudo apt-get update`
2. Instalar o pacote docker.io :
`sudo apt-get -y install docker.io`
3. Para rodar o docker automaticamente quando o Ubuntu inicia:
`sudo update-rc.d docker defaults`
4. Roda o docker (se não tiver rodando ainda):
`sudo service docker start`
5. Teste a instalação do docker:
`sudo docker run hello-world`


## Inicializando containers
Opção `run` com interatividade:

* $ docker run -it nome_da_imagem [comando]

Executando em background:
* $ docker run -d nome_da_imagem

Eliminando após o uso:
* $ docker run --rm -it nome_da_imagem [comando]


## Criando imagens
Iniciar container interativo:
* $ docker run -it ubuntu

Realizar alterações:
* $ sudo apt-get update && apt-get install -y nome_do_pacote

Encerrar e commitar
* $ docker commit [id] nome_da_imagem

## Dockerfile
* $ docker build -t nome_da_imagem
	* Dentro do Dockerfile:
>> FROM [imagem da qual será herdado]
>> RUN [instalação de pacotes]
>> EXPOSE [abertura de portas]
>> CMD [execução de comandos]

### Gerando nossas próprias imagens com a opção build seguida de user/serviço e docker le
* $ docker build -t user/serviço [caminho]

### Utilizando imagens prontas
Podemos buscar em repositórios o ciais e não o ciais em Login (https://hub.docker.com/login/)
* $ docker login

Baixando as imagens
* $ docker pull nome_da_imagem

Buscando imagens
* $ docker searche nome_da_imagem

Enciando imagens
* $ docker push user/serviço

# Docker COMPOSE
Verifique se possuí instalado na maquina:
* $sudo apt-get install docker-compose

Crie um diretorio e dentro crie um aquivo chamado docker-compose.yml. Tal arquivo de manifesto será controlado pelo docker compose, o qual é uma ferramenta de complemento dentro do Docker. Comecemos a editar o arquivo:

>> db:
>>    image: mysql
>>    volumes:
>>    - ./database/:/var/lib/mysql/
>>    environment:
>>        - MYSQL_ROOT_PASSWORD=SUASENHA
>>
>> blog:
>>    image: wordpress
>>    volumes:
>>    - ./localhost/:/var/www/html/    
>>    environment:
>>        - WORDPRESS_DB_PASSWORD=SUASENHA
>>    links:
>>        - db:mysql
>>    ports:
>>        - 80:80

### Iniciando em modo normal
* docker-compose up

Inidiando em modo silent
* docker-compose up -d

Matando a imagem:
* docker-compose kill

Removendo Imagem:
* docker-compose rm

Inspecionando imagem:
* docker inspect mysql
