---
layout: post
title: DSpace em um CentOS 5.3
date: '2009-07-15 00:58:19'
---


Novamente estou eu implantando o DSpace em um servidor Linux, desta vez um CentOS 5.3, um sistema operacional baseado nos pacotes disponibilizados pelo Red Hat Linux. Mas desta vez é a versão 1.5, ao invés da 1.4. Hora de desbravar [novos](http://seiti.eti.br/blog/2009/resolvendo-o-problema-da-busca-no-dspace) [bugs](http://seiti.eti.br/blog/2009/bug-no-plugin-de-estatisticas-do-uminho-para-o-dspace)…

O [DSpace](http://www.dspace.org) é uma biblioteca digital, mas pode ser encarado como uma ferramenta de gestão de documentos eletrônicos. No entanto sua construção tem como objetivo organizar e tornar acessível material técnico e científico, que por sua vez são incluídos no sistema pelos próprios autores (*self-archiving*).

Da versão 1.4 para a versão 1.5 ocorreram inúmeras mudanças. Dentre elas a adoção do Maven, para tratar das dependências de bibliotecas Java, e o estabelecimento de uma interface XML/XSLT denominada Manakin, embora a antiga interface em JSP continue sendo distribuído e funcionando.

Relato aqui então particularidades da instalação com relação ao CentOS. Detalhes e uma melhor descrição da instalação podem ser vistos na [documentação oficial](http://www.dspace.org/1_5_2Documentation/).

Primeiro é necessário ter um ambiente Java. Optei pelo OpenJDK mesmo, pela facilidade de instalação e atualização. Não vi necessidade em utilizar o Sun JDK. Diferente dos Debian e Ubuntus da vida, a família Red Hat utiliza o **yum** para gerenciar seus pacotes. Mas seu uso é bem intuitivo para quem está acostumado com o *apt-get*:

yum search jdk yum install java-1.6.0-openjdk.i386

Após instalado lembre-se de verificar se tudo correu bem:

java -version

> java version “1.6.0”  
>  OpenJDK Runtime Environment (build 1.6.0-b09)  
>  OpenJDK Client VM (build 1.6.0-b09, mixed mode)

Java instalado, vamos colocar no ar o banco de dados PostgreSQL:

yum search postgres yum install postgresql-server.i386 yum install postgresql.i386

service postgresql start

Os arquivos de configuração do PostgreSQL ficam em <tt>/var/lib/pgsql/data/</tt>.

Para criar um usuário dspace e configurar sua senha no CentOS:

useradd dspace passwd dspace

Vamos agora habilitar o sudo para o usuário dspace, pois não gosto de ter de logar como root a todo momento

visudo

Incluindo a seguinte linha. Estas permissões podem ser restringidas depois:

> dspace ALL=(ALL) ALL

Testando o novo usuário dspace e seu acesso ao **sudo**:

su - dspace sudo touch bla

Infelizmente, ao testar o sudo, surgiu este erro:

> Erro: sudo must setuid root

Esquisito… Parece que não configuraram direito o sudo na distribuição do CentOS. O que ocorre é que eu não podia sequer executar o binário. Resolvido com o comando

chmod 4111 /usr/bin/sudo

Agora instalemos o **tomcat**:

yum install tomcat5

Voltando um pouco ao banco de dados. Agora que temos o usuário no CentOS, vamos definir um banco de dados para ele, com as permissões necessárias.

root# createuser -U postgres -d -A -P dspace dspace$ createdb -U dspace -E UNICODE dspace

Não esquecer de editar o arquivo <tt>/var/lib/pgsql/data/postgresql.conf</tt> neste trecho, habilitando o acesso via TCP:

> listen_addresses = ‘localhost’  
>  port = 5432

E o arquivo <tt>/var/lib/pgsql/data/pg_hba.conf</tt>, possibilitando o acesso de usuários locais mediante senha com hash em MD5:

> host all all 127.0.0.1/32 md5

### Maven 2

Agora vamos baixar o Maven 2 e instalá-lo. Desta vez temos de deixar de lado o yum e suas facilidades:

wget http://linorg.usp.br/apache/maven/binaries/apache-maven-2.2.0-bin.zip unzip apache-maven-2.2.0-bin.zip sudo cp -R apache-maven-2.2.0 /usr/local/ ln -s /usr/local/apache-maven-2.2.0 /usr/local/maven

Edite o <tt>~/.bashrc</tt> com o seguinte conteúdo, definindo algumas variáveis de ambiente para facilitar sua vida:

> export M2_HOME=/usr/local/maven  
>  export PATH=${M2_HOME}/bin:${PATH}  
>  export JAVA_HOME=/etc/alternatives/java_sdk #uso o Java Open JDK, mude esta linha caso seu JVM seja outro

Recarregue o bashrc para que as variáveis de ambiente tomem efeito:

source ~/.bashrc

Seguindo o restante das instruções do DSpace encontrei mais um problema. Após rodar o **mvn package** foi criado o projeto pronto para compilação e deploy. Mas ao rodar o ant, com o comando **ant fresh_install** foi mostrada a seguinte mensagem de erro:

> BUILD FAILED  
>  /home/dspace/dspace-1.5.2-release/dspace/target/dspace-1.5.2-build.dir/build.xml:88: No supported regular expression matcher found

Parece que faltou ao **ant** alguma biblioteca, que pode ser instalado através do yum:

sudo yum install ant-apache-regexp

Bom, mesmo assim apareceu outro erro:

> Interpolation failed in value of property “db.name”, there is no property named “postgres”

Que interpretei como algum problema na geração do **dspace.cfg**. Verificando o dito cujo substitui:

> db.name = ${postgres}

por

> db.name = ${postgres}

Segui normalmente o restante da [documentação do DSpace](http://www.dspace.org/1_5_2Documentation/), mas na hora de [agendar algumas tarefas](http://www.dspace.org/1_5_2Documentation/ch03.html) no CentOS, era apresentado um erro:

crontab -e

> cron/dspace: Permission denied

O jeito foi executar o comando como **root**:

sudo crontab -e -u dspace

Outro problema ocorreu com o envio de emails, que gerava o erro: **javax.mail.NoSuchProviderException: smtp**  
 Resolvido removendo a seguyinte biblioteca Java, que parece entrar em conflito com a contida no DSpace:

sudo unlink /var/lib/tomcat5/common/lib/\[javamail\].jar sudo /etc/init.dtomcat5 restart


