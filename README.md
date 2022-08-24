
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
 4) Acesse o RabbitMQ na URL http://localhost:15672. O login padrão é guest e a senha é guest.

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


Acessando a ajuda do comando rabbitmqadmin:

rabbitmqadmin help subcommands
rabbitmqadmin --help
rabbitmqctl --help
Listando os exchanges existentes no RabbitMQ:

rabbitmqadmin list exchanges
Listando as filas existentes no RabbitMQ:

rabbitmqadmin list queues
Listando as filas existentes no RabbitMQ com mais detalhes:

rabbitmqadmin -f long list queues
rabbitmqadmin -f long -d3 list queues
Listando os bindins existentes no RabbitMQ:

rabbitmqadmin -f long -d3 list bindings
Listando os vhosts existentes no RabbitMQ:

rabbitmqadmin list vhosts
Listando os usuários existentes no RabbitMQ:

rabbitmqadmin list users
Adicionando um exchange com o nome ‘app1‘ e o tipo ‘direct‘ no vhost ‘/‘:

rabbitmqadmin declare exchange name=app1 type=direct durable=true --vhost=/
Adicionando uma fila com o nome ‘logs_app1‘, durável e o tipo ‘direct‘ no vhost ‘/‘

rabbitmqadmin declare queue name=logs_app1 durable=true --vhost=/
Adicionando um bind entre o exchange ‘app1‘ e a queue ‘logs_app1‘ com a routing_key ‘app1-logs_app1‘:

rabbitmqadmin declare binding source=app1 destination=logs_app1 routing_key=app1-logs_app1
Adicionando um usuário ao rabbitmq com o nome ‘user_app1‘ com permissão de ‘administrator‘:

rabbitmqctl add_user user_app1 SENHA
rabbitmqctl set_user_tags user_app1 administrator
rabbitmqctl set_permissions -p / user_app1 "." "." "." 
rabbitmqctl set_topic_permissions -p / user_app1 app1 "." ".*"
Altere a senha do usuário guest:

rabbitmqctl change_password guest NOVA-SENHA
Definindo o nome do cluster RabbitMQ para ‘rabbit@rabbitmq-master’:

rabbitmqctl set_cluster_name rabbit@rabbitmq-master
Exportando a configuração (lembre-se de salvar em um diretório ou volume comum ao conteiner e ao host)

rabbitmqadmin -H localhost -u guest -p SENHA export /tmp/rabbit.config
Importando a configuração (lembre-se de montar um diretório ou volume comum ao conteiner e ao host):

rabbitmqadmin -q import /tmp/rabbit.config
Visualizando a quantidade de mensagens numa fila:

rabbitmqadmin -H localhost -u guest -p SENHA get queue=logs_app1 count=10
Observação:
A partir do momento que a senha do usuário guest foi alterada, se faz necessário adicionar os parâmetros -H localhost -u guest -p SENHA em qualquer comando do rabbitmqadmin.

Esta entrada foi publicada em Uncategorized com as palavras-chave docker, rabbitmq. Adicione o link permanente aos seus favoritos.