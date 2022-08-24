
## url to site that teach how install rabbitmq with container Docker
https://blog.aeciopires.com/instalando-o-rabbitmq-via-docker/


## command to pull the image Docker of RabbitMQ.
VERSAO=3-management
export VERSAO
docker pull rabbitmq:$VERSAO

## command to create container docker
docker run -d --name rabbitmq  -p 5672:5672  -p 15672:15672  --restart=always  --hostname rabbitmq-master \
 -v /home/francisco/estudos/rabitmq/data:/var/lib/rabbitmq  rabbitmq:$VERSAO


 ## Many informations about the subject
 4) Acesse o RabbitMQ na URL http://IP-Servidor:15672. O login padrão é guest e a senha é guest.

5) Se quiser parar o conteiner, é só executar o comando abaixo.

docker stop rabbitmq
6) Para iniciá-lo novamente, execute o comando abaixo.

docker start rabbitmq
7) Para visualizar os logs, execute o comando abaixo.

docker logs -f rabbitmq
Mais informações sobre o RabbitMQ e como configurá-lo podem ser encontradas nos links abaixo.

https://www.rabbitmq.com/documentation.html
http://blog.aeciopires.com/primeiros-passos-com-rabbitmq/

Caso não consiga acessar o RabbitMQ via interface Web, pode gerenciá-lo pela linha de comando.

Acessando o prompt de comandos do conteiner rabbitmq

docker exec -it rabbitmq /bin/bash