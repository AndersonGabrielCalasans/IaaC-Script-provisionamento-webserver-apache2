# 📘 Infraestrutura como código: Script de provisionamento de um servidor web (apache) 

Laboratório proposto pelo professor Denilson Bonatti, Tech Lead da DIO, no curso de introdução ao ambiente Linux onde subimos uma aplicação em um servidor web usando infraestrutura como código em um script de provisionamento de execução.

## O que é?

Infraestrutura como código (IaC) é o gerenciamento e provisionamento da infraestrutura por meio de códigos, em vez de processos manuais.

Com a IaC, são criados arquivos de configuração que incluem as especificações da sua infraestrutura, facilitando a edição e a distribuição de configurações. Ela também assegura o provisionamento do mesmo ambiente todas as vezes. 

## Controle de versão

O controle de versão é uma parte importante da IaC. Os arquivos de configuração devem pertencer à fonte como qualquer outro código-fonte de software. Ao implantar a infraestrutura como código, também é possível separá-la em módulos, que podem ser combinados de diferentes maneiras por meio da automação.

## Passos realizados

 1- **Subir uma máquina virtual:**
 	
 A máquina utilizada para realizar o projeto foi subida na nuvem da GCP com as seguintes configurações:
```
gcloud compute instances create webserver 
--project=inner-precept-366512 
--zone=us-west1-b 
--machine-type=e2-micro 
--network-interface=network-
tier=PREMIUM,subnet=default --maintenance-policy=MIGRATE --provisioning-model=STANDARD 
--service-account=787341881121-compute@developer.gserviceaccount.com --
scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://w
ww.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append 
--tags=http-server --
create-disk=auto-delete=yes,boot=yes,device-name=webserver,image=projects/debian-cloud/global/images/debian-11-bullseye-
v20220920,mode=rw,size=10,type=projects/inner-precept-366512/zones/us-west4-b/diskTypes/pd-balanced --no-shielded-secure-boot 
--shielded-vtpm --shielded-integrity-
monitoring --reservation-affinity=any
```
 2- Atualizar o servidor:
 3- Instalar o apache2;
 4- Instalar o unzip;
 5- Baixar a aplicação disponível em um diretório do GitHub /tmp;
 6- Copiar os arquivos da aplicação no diretório padrão do apache;
 7- Subir arquivo de script para um repositório no GitHub.

 Para os passos anteriores nó criamos um script para execução que se encontra [aqui](https://github.com/AndersonGabrielCalasans/IaaC-Script-provisionamento-webserver-apache2/blob/main/script-iac-webserver.sh). 
 Para você utilizá-lo para subir sua aplicação, baixa alterar o endereço do diretório do arquivo no script modelo e seguir os passos a seguir:

 - Crie uma pasta na raíz com o nome **script**.
 	```
	cd /
 	sudo mkdir script
	```
 - Entre na pasta criada e crie o script padrão com nome **script-iac-webserver.sh**.
 	```
	cd /script
 	sudo nano script-iac-webserver.sh
	```
 - Copie o script padrão, altere o endereço da sua aplicação web de acordo com o diretório onde ela se encontra (copie o link.zip), salve o arquivo e feche.

 - Conceda ao script **permissão de execução**.
 	```
	sudo chmod +x script-iac-webserver.sh
	```
 - Execute o script. **Importante:** É recomendável que realize uma snapshot do que realizou até agora por segurança, pois caso tenha errado algum passo você consegue alterar e voltar ao passo anterior.
 	```
	sudo ./script-iac-webserver.sh
	```
Tudo certo, agora iremos subir o projeto para um repositório no **GitHub:**

- Verificando se o Git está instalado na VM:
          
        apt install git -y

- Configurando o git:

        git config —global [user.email](http://user.email) “[EMAIL]”
        git config —global [user.](http://user.email)name “[NOME DO USUÁRIO]”

- Subindo o projeto:

        git init
        git add .
        git commit -m “Arquivos IaC v.1”
        git branch -M main
        git remote add origin [git@github.com](mailto:git@github.com):AndersonGabrielCalasans/LinuxProject-InfraAsACode.git
        git push -u origin main

## Autor
	
	Anderson Gabriel Calasans
