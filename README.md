# Projeto-GLPI
Instalação do GLPI versão 9.3.1 e implementação do Fusion Inventory versão 9.3+1.2

### A instalação dos arquivos podem ser feitas através do git clone ou na própria documentação. 



# Dependências:
    sudo apt-get install ca-certificates apache2 libapache2-mod-php7.0 php7.0-cli php7.0 php7.0-curl php7.0-apcu php7.0-gd php7.0-imap php7.0-ldap php7.0-mysql php-cas php7.0-soap php7.0-mbstring php7.0-xml php7.0-xmlrpc mariadb-server
### (Caso você utilize Ubuntu Server ou derivados, dê um search no php para verificar em qual versão está. No momento 7.2)
  
 # Instalação do GLPI através do wget: 
    wget https://github.com/glpi-project/glpi/releases/download/9.3.1/glpi-9.3.1.tgz
  
 # Extraindo e movendo o GLPI para pasta WEBServer:
  ## Extração:
      tar -xf glpi-9.3.1.tgz
  ## Movendo:
      mv glpi-9.3.1.tgz /var/www/html/
 
 # Setando permissões:
     chown www-data:www-data /var/www/html/glpi -Rf
     chmod 775 /var/www/html/glpi -Rf
     
 # Criação do banco de dados:
    mysql -u root -p
 
    create database glpidb; // Criação do banco de dados
    create user 'glpi'@'localhost' identified by 'escolhaumasenha'; // Criação de user e passwd
    grant all on glpidb.* to 'glpi'@'localhost'; // garantindo todos os privilégios para o user
    flush privileges; // ativando os privilégios
    quit // saindo do ambiente banco de dados
    
  # Configuração do Apache2:
    nano /etc/apache2/sites-available/glpi.conf // Arquivo de configuração do apache2
   ## Configuração (copia e cola dentro do nano): 
        <Directory /var/www/html/glpi>
         AllowOverride All
        </Directory>
        <Directory /var/www/html/glpi/config>
        Options -Indexes
         </Directory>
        <Directory /var/www/html/glpi/files> Options -Indexes
        </Directory>
   ## Salva e quita do nano:
      CTRL + O depois CTRL + X
   ## Aplicando a configuração do Apache2:
      a2ensite glpi
      
   ## Reiniciando o Apache2:
      /etc/init.d/apache2 restart // Será necessária a autênticação do usuário
  
  # Teste do servidor:
      seuip/glpi
   ### exemplo: 192.168.2.123/glpi
   ### Caso dê algum erro, provavelmente outro serviço está utilizando a porta 80
      sudo lsof -i :80 // Verificando serviços utilizando a porta :80
      sudo kill PID // Exemplo: nginx pid 950 // sudo kill 950
   ### Depois de efetuar esses procedimentos reinicie o apache e tente novamente.      
      /etc/init.d/apache2 restart

