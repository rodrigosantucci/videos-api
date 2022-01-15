### INSTALACAO DO JAVA JDK
Copiar arquivos install-java.sh e openjdk-14_linux-x64_bin.tar.gz para o servidor e executar os seguintes comandos: 

# Dar permissão de escrita
sudo chmox +x install-java.sh
sudo ./install-java.sh -f openjdk-14_linux-x64_bin.tar.gz

## configuração etc/enviroment e bashrc
 
sudo vim /etc/enviroment
source /etc/environment
escrever:
JAVA_HOME="/usr/lib/jvm/jdk-14"

e no arquivo .bashrc: 
sudo vim ~/.bashrc
escrever:
export JAVA_HOME="/usr/lib/jvm/jdk-14"

### Instalacao do Gradle
Copiar arquivos tar.gz do gradle-7.3.3-bin.zip para o servidor

sudo mkdir /opt/gradle
sudo unzip -d /opt/gradle gradle-7.3.3-bin.zip
export PATH=$PATH:/opt/gradle/gradle-7.3.3/bin



## Definir as propiedades do banco MySQL no arquivo application.properties

DATABASE_HOST=127.0.0.1
DATABASE_PORT=3306
DATABASE_NAME=videoapi
DATABASE_USER=rodrigo
DATABASE_PASSWORD=xxxxxx

## Criar Banco e Tabelas

```sql
#create database
CREATE DATABASE videoapi;

#switch to newly created database
USE videoapi;

#create users table
CREATE TABLE `users` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `username` varchar(45) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `password` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `created` datetime DEFAULT NULL,
  `modified` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `username` (`username`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

#create videos table
CREATE TABLE `videos` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `user_id` int(10) unsigned NOT NULL,
  `title` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `size` double DEFAULT NULL,
  `url` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `created` datetime DEFAULT NULL,
  `modified` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_videos_users_idx` (`user_id`),
  CONSTRAINT `fk_videos_users` FOREIGN KEY (`user_id`) REFERENCES `users` (`id`) ON DELETE CASCADE ON UPDATE NO ACTION
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```


###Dentro da pasta da api executar o comandos

## Buildar aplicação 
./gradlew clean
./gradlew build

## Rodando a aplicação
./gradlew bootRun


##Link da Documentação da API no Swagger
http://localhost:8080/swagger-ui.html


## Listar serviços e portas em uso
sudo lsof -i -P -n


