# Projeto-GLPI
Instalação do GLPI versão 9.3.1 e implementação do Fusion Inventory versão 9.3+1.2

### A instalação dos arquivos podem ser feitas através do git clone ou na própria documentação. 

# Dependências:
    sudo apt-get install ca-certificates apache2 libapache2-mod-php php-cli php php-curl php-apcu php-gd php-imap php-ldap php-mysql php-cas php-soap php-mbstring php-xml php-xmlrpc mariadb-server    

  
 # Instalação do GLPI através do wget: 
    wget https://github.com/glpi-project/glpi/releases/download/9.3.1/glpi-9.3.1.tgz
 ### A versão atualiza conforme o tempo, essa instalação está adequada para GLPI 9.3.1
  
 # Extraindo e movendo o GLPI para pasta WEBServer:
 
  ## Extração:
      tar -xf glpi-9.3.1.tgz
      
  ## Movendo:
      mv glpi-9.3.1 /var/www/html/
 
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

   # Vídeo explicativo sobre instalação do Fusion Inventory:
      https://youtu.be/DB6cKgVVFCA
      
   # Fusion Inventory Releases para GLPI 3.2.1
    https://github.com/fusioninventory/fusioninventory-for-glpi/releases/download/glpi9.3%2B1.2/fusioninventory-9.3+1.2.tar.gz



## Referências: 
    https://wiki.projetoroot.com.br/index.php?title=GLPI
    https://glpi-project.org/pt-br/
    http://fusioninventory.org/


### Felipe Austríaco - Redes ~ Fatec Osasco
![](https://github.com/w1redl4in/.dotfiles/blob/master/Prints/2019-02-27--07:12:36:PM--1600900--scrot.png)
