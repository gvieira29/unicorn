# INSTALAÇÃO DO MEDIAWIKI

O MediaWiki é um modelo de Wiki OpenSource.  
Confira o [Site Oficial](https://www.mediawiki.org/wiki/MediaWiki).

## Montando um Servidor Web

**Para fazer a instalação da Wiki, vamos configurar um servidor web (caso não tenha ainda). Siga estas etapas:**  

- Voce pode instalar o pacote LAMP, que  pode ser feito através do comando `# apt install -y lamp-server^`, mas este guia ira mostrar como baixar os pacotes separadamente
  ```
  # apt install -y lamp-server^
  ```

- **Instalar o apache:** 
  ```
  # apt install -y apache2
  ```
  Pronto, o apache esta instalado.  
  Agora dê acesso ao diretório utilizando:  
  ```
  # chmod 777 /var/www
  ```

- **Instalar o PHP:**    
  ```
  # apt install -y libapache2-mod-php php php-cli php-common php-gd php-intl php-mbstring php-pear php-xml php-zip
  ```
  Para verificar se está funcionando corretamente, crie uma pagina de teste:  
  ```
  ~$ echo "<?php phpinfo(); ?>" >> teste.php
  ~$ cp teste.php /var/www/html
  ~$ service apache2 restart
  ```
  Agora acesse **localhost/teste.php** ou **127.0.0.1/teste.php** para verificar a página que criamos.  

- **Instalar o Banco de Dados: vamos utilizar o MySQL mas também pode ser usado MariaDB para este projeto.**  
  ```
  # apt install -y mysql-client mysql-server php-mysql
  ```
  Com o MySQL Instalado, abra com o comando:
  ```
  # mysql
  ```
  - Para verificar se esta funcionando, digite o comando:
    ```
    SHOW DATABASES;
    ```
  - **Crie um novo banco:**
    ```
    CREATE DATABASE bancowiki;
    ```
    Para deletar um banco, utilize:
    ```
    DROP DATABASE bancowiki;
    ```
  - **Crie um usuario e senha para seu banco:**
    ```
    CREATE USER 'usuario1234'@'localhost' IDENTIFIED BY 'senha1234';
    ```
  - **De as permissoes para o usuario:**
    ```
    GRANT ALL PRIVILEGES ON *.* TO 'usuario1234'@'localhost' WITH GRANT OPTION;
    ```
  - **Rode o comando para atualizar:**
    ```
    FLUSH PRIVILEGES;
    ```
- **Instalar o *PHPMYADMIN***
  ```
  # apt install -y phpmyadmin
  ```
  Durante o processo, ira perguntar qual servidor deseja usar para executar o ***phpmyadmin***, selecione o **apache2** marcando com a tecla **ESPAÇO**, usando a tecla **TAB** mova o cursor para o **OK**. Confirme com **Sim**.  

  O ***phpmyadmin*** deve estar funcionando, para testar vá até o navegador e acesse **localhost/phpmyadmin** ou **127.0.0.1/phpmyadmin**, para fazer login, utilize usuario e senha cadastrado no **MySQL** que criamos no passo anterior.  

## Instalação do MediaWiki

- **Primeiro é necessário ter o pacote baixado, [link para o arquivo](https://www.mediawiki.org/wiki/Download).**
```
# wget https://releases.wikimedia.org/mediawiki/1.33/mediawiki-1.33.0.tar.gz
```
- **Extraia o pacote:**
```
# tar -xf mediawiki-1.33.0.tar.gz
```
- **Renomeie a pasta para *html*:**
```
# mv mediawiki-1.33.0 html
```
- **Siga estes passos:**
```
# rm -R /var/www/html
# cp -R /home/seu_usuario/html /var/www/
```
Feito isso, vá até o navegador e acesse **localhost** ou **127.0.0.1**, O MediaWiki estará pronto para ser configurado.  
Nesse primeiro momento deverá ser feito a criação e configuração do arquivo ***LocalSettings.php***.  