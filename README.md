# Automação com a ferramenta Ansible

# Para Rodar o arquivo da avaliação final siga os passos a seguir

# passo 0 - Clone do repositorio e entrar na pasta do projeto
git clone https://github.com/Menosse/iaac-mba-clcdevops.git

# passo 1 - Iniciar e configurar as virtuais
Iniciar como máquinas virtuais
Vagrant

# Rodar o script de instalação do ansible e outras dependências
# Script de inicializacao Maquina iaac
#Abra um novo terminal

ssh iaac vagrant

cd /vagrant

sudo sh iaac.sh

# Exportar o ansible.cfg nas maquinas
export ANSIBLE_CONFIG="./ansible.cfg"

# Script de inicializacao Maquina server
# Abra um novo terminal

servidor ssh vagrant

cd /vagrant

sudo sh server.sh

# Criar chave ssh e permitir o acesso da maquina iaac na maquina server
# Na maquina iaac, crie uma chave

ssh-keygen

# Copiar a chave

cat /home/vagrant/.ssh/id_rsa.pub

# Entrar na maquina server e colar o conteúdo a chave arquivo no arquivo /home/vagrant/.ssh/authorized_keys

sudo nano /home/vagrant/.ssh/authorized_keys

Conferir se a chave foi colada corretamente

cat /home/vagrant/.ssh/authorized_keys

Abra o arquivo "$ sudo vi /etc/ssh/sshd_config" e procure pela linha "PasswordAuthentication no" e mude para "yes" e salve o arquivo.

sudo nano /etc/ssh/sshd_config

Após salvar o arquivo autorize o serviço do sshd

sudo systemctl reiniciar ssh

# passo 2 - Rodar o playbook de instalação da aplicação
# Na maquina iaac

cd ansible_slackio/

ansible-playbook playbook.yml

# Para atualizar a aplicacao
ansible-playbook playbook.yml --tags update_app
