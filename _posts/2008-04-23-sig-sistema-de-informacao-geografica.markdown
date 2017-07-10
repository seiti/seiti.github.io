---
layout: post
title: SIG - Sistema de Informação Geográfica
date: '2008-04-23 19:48:31'
tags:
- geo
- gis
---


![image](../../wiki/images/brave-gnu-world.jpg "WikiImage")Um SIG trata-se de um **Sistema de Informação Geográfica**, ou também **Sistema de Informação Geoespacial**.

Dois sistemas livres amplamente utilizados são o MapServer e o GeoServer. Conheço um pouco (**bem** pouco, na verdade) o MapServer e desconheço o outro. Minha intenção é documentar, nesta página, todo o processo para a instalação e configuração de ambos.

O [MapServer](http://mapserver.gis.umn.edu/)<span></span> é um WMS que roda como *cgi*, mas possui alguns módulos que dão suporte a algumas linguagens, como o PHP, e rodar diretamente do servidor Apache.

O [GeoServer](http://www.geoserver.org/)<span></span> é uma aplicação java, que por esta razão necessita de um servidor de aplicações java para web. Além disso ele tem a possibilidade de, assim como o MapServer, obter dados a partir do PostGis

O **PostgreSQL**, ou postgres, é um banco relacional amplamente conhecido e utilizado. O **PostGIS** é um conjunto de extensões ao postgres que lhe confere a capacidade de realizar cálculos e armazenamento de informações georeferenciadas.


## Ambientando-se

<div>> ### Alguns acrônimos e definições
> 
> - **OGC** – [Open Geospatial Consortium](http://www.opengeospatial.org/)<span></span> – padroniza os tipos de dados utilizados pelos diversos SIGs;
> - **WMS** – Web Map Service – através de pedidos embutidos em requisições em URLs, um WMS deve prover: metadados sobre o próprio serviço, um mapa geográfico e, opcionalmente, informações sobre itens particulares no mapa;
> - **WFS** – Web Feature Service – descreve operações sobre dados geográficos e suas características (*features*, dados que podem ser gerados para se criar mapas geográficos);
> - **WCS** – Web Coverage Service – agregando os serviços acima, permite a busca e transformações sobre os dados obtidos em uma rede de aplicações geográficas distribuídas;
> - **CS-W** – Catalog Service Web – padroniza a interface utilizada para consultar os serviços supracitados;
> - **SFS** – Simple Features – SQL – define como digitalizar informações geográficos, geralmente em um banco de dados relacional (*point*, *linestring*, *polygon* etc.);
> - **GML** – Geography Markup Language – um XML para transporte de dados geográficos.
> - **SRS** – Spatial Reference System, no contexto da OGC, são codificados na sintaxe definida pela EPSG (European Petroleum Survey Group). O SRS padrão definido pela OGC é 4326 (WGS84, World Geodetic System, grau decimal).

Vamos agora criar um ambiente de avaliação e desenvolvimento de sistemas SIG dentro do **Ubuntu**. Primeiro devemos proceder com a instalação dos pacotes <tt>postgresql, postgis, postgresql-8.2-postgis, libpostgis-java, sun-java5-bin</tt>.

Entre os outros pacotes instalados automaticamente está o **proj4**, que reúne bibliotecas e programas de conversão de dados.

Bom, após a instalação do Java pode ser necessário configurar a máquina virtual java padrão do sistema. Isto é feito, no Ubuntu, através do comando *update-java-alternatives*.

</div>### GeoServer

O **Jetty** é um servidor de aplicações java web escrito 100% em java. É conhecido por seu desempenho, em contraste com o [ApacheTomcat](../../wiki/ApacheTomcat/edit "Create this page"). Uma opção para rodar o [GeoServer](http://www.geoserver.org/)<span></span> é baixar o [pacote binário](http://docs.codehaus.org/display/GEOS/Latest)<span></span> e rodá-lo a partir do servidor Jetty embarcado no próprio GeoServer:

<div style="font-family: monospace;"><span>cd</span> /opt  
 sudo unzip -xvzf geoserver-*-bin.zip  
 sudo <span>export</span><span>JAVA_HOME=</span><span>‘/usr/lib/jvm/java-1.5.0-sun’</span>  
 sudo <span>export</span><span>GEOSERVER_HOME=</span><span>‘/opt/geoserver’</span>  
 sudo <span>$GEOSERVER_HOME</span>/bin/startup.sh</div>Aponte seu navegador para [http://localhost:8080/geoserver](http://localhost:8080/geoserver) e poderá ver seu servidor GeoServer rodando. Para se entrar na área restrita o nome de usuário é <span>*admin*</span> e a senha é <span>*geoserver*</span>.

Outra opção é pegar o pacote **war** e implantá-lo no [ApacheTomcat](../../wiki/ApacheTomcat/edit "Create this page"). Com o Tomcat rodando, entre em sua interface de gerenciamento, provavelmente [http://localhost:8180/manager](http://localhost:8180/manager) para fazer o deploy. Talvez seja preciso editar as *políticas* de sistema para que tudo funcione, como pode [ser visto](http://grimmeister.wordpress.com/2007/08/08/setting-up-an-open-geospatial-consortium-service-server/) no Southern Tip blog.

Caso você tenha *shapefiles* para testar, recomendo [este tutorial](http://geoserver.org/display/GEOSDOC/User+Tutorial+Shapefile).

### PostGIS

[![PostGIS logo](http://www.spatiallyadjusted.com/media/images/2005/adbadge_square_240.gif "WikiImage")](http://postgis.refractions.net/)No Ubuntu, após instalar o pacotes referentes ao PostgreSQL e ao PostGIS é preciso executar o seguinte procedimento para criar um *template* no postgres habilitado a executar funções SIG:

Entre como o usuário <tt>postgres</tt>:

<div>sudo su - postgres

</div>Crie um banco de dados. Coloque o sufixo *template_* para facilitar tua vida:

<div style="font-family: monospace;">createdb template_gis</div>Habilite a linguagem *plpgsql* para criação de *stored procedures*:

<div style="font-family: monospace;">createlang plpgsql -d template_gis</div>Alimente o banco com as funções e tabelas de referência do sistema SIG (serão criadas várias funções e inserções no banco, aguarde):

<div style="font-family: monospace;">psql template_gis -f /usr/share/postgresql<span>-8.2</span>-postgis/lwpostgis.sql  
 psql template_gis -f /usr/share/postgresql<span>-8.2</span>-postgis/spatial_ref_sys.sql</div>Entre no banco criado (isto abrirá um terminal de comandos do postgresql):

<div style="font-family: monospace;">psql template_gis</div>Finalmente transforme o banco criado em um template:

<div style="font-family: monospace;"><span>UPDATE</span> pg_database <span>SET</span> datistemplate=<span>‘true’</span><span>WHERE</span> datname=<span>‘template_gis’</span>;</div>Saia do terminal do postgres:

<div>\q

</div>A partir daí pode-se criar novo bancos SIG a partir do nosso template criado. Recomendo a utilização do pgAdmin III (pacote <tt>pgadmin3</tt>).

**Atenção**: caso ainda não tenha feito, é preciso criar uma senha para o usuário *postgres* no próprio banco de dados. Abra um terminal de comando do postgres:

<div style="font-family: monospace;">sudo -u postgres psql template1</div>Altere a senha do usuário postgres:

<div style="font-family: monospace;"><span>ALTER</span> USER postgres <span>WITH</span> PASSWORD <span>‘secret’</span>;  
 \q</div>E se for necessário logar no postgres remotamente, isto é, via tcp/ip a partir de outra máquina (útil para separar o banco de dados da aplicação SIG), é preciso editar o arquivo <tt>/etc/postgresql/8.2/main/postgresql.conf</tt>:

<div>#listen_addresses = 'localhost' listen_addresses = '*' #isto faz com que o postgres aceite conexões de outros endereços de rede

</div>E o arquivo <tt>/etc/postgresql/8.2/main/pg_hba.conf</tt>:

<div>#IPv4 local connections: #qualquer computador com endereço 192.168.0.* se conecta se tiver um usuário configurado no postgres host all all 192.168.0.0/24 md5

</div><div>
## GeoServer: Configuração e testes

</div><div style="float: right;"><span style="width: 315px;">GeoServer</span></div>Para carregar *shapefiles* siga os passos contidos neste ótimo [tutorial](http://docs.codehaus.org/display/GEOSDOC/User+Tutorial+Shapefile). Só houve um problema que ocorreu comigo foi do sistema não encontrar automaticamente o número EPSG ([Wikipedia:EPSG](http://en.wikipedia.org/wiki/EPSG)). Tive de obter a listagem gerada pelo próprio GeoServer e buscar o número correspondente aos dados.

### Shapefiles no PostGIS

Para carregar os shapefiles no postgis é preciso utilizar o programa **shp2pgsql**, instalado com os pacotes referentes ao postgis:

<div style="font-family: monospace;">shp2pgsql -s SRID arquivo.shp nom_tabela > arquivo.sql</div>Onde SRID é um número que você deve encontrar da seguinte maneira:

- Abra o arquivo <tt>.prj</tt> em um editor de texto. Você encontrará algo como:

<div>PROJCS["SAD_1969_UTM_Zone_23S",GEOGCS["GCS_South_American_1969",DATUM["D_South_American_1969",SPHEROID["GRS_1967_Truncated",6378160.0,298.25]] e UNIT["Degree",0.0174532925199433]

</div>- Abra a ferramenta de consulta do PgAdmin III e entre com a seguitne consulta (pode demorar alguns segundos):

<div>select srid, srtext, proj4text from spatial_ref_sys where srtext ILIKE '%SAD_1969%'

</div>- Anote o **srid** (no caso 29193) da entrada mais próxima do esperado.

Referência: [started with PostGIS http://www.bostongis.com/?content_name=postgis_tut01](../../wiki/Getting/edit "Create this page")

Isto criará um arquivo de comandos SQL <tt>arquivo.sql</tt>. Tive outros problemas ao tentar executar os comandos contidos no arquivo SQL: ele não estava em **utf8**, e sim em **latin1**; e o usuário *geo_user* que criei não tinha as permissões necessárias para criar tabelas no banco.

Bom, como meu banco está em utf8 tive de converter o arquivo SQL com o seguinte comando:

<div style="font-family: monospace;">iconv  -f latin1 -t utf8  -o arquivo.sql2  arquivo.sql</div>Quanto às permissões, é preciso conceder ao usuário em questão acesso à tabela **geometry_columns**, pois ela controla as colunas com as geometrias (pontos, linhas, polígonos) das demais tabelas no banco em que se deseja guardar informações geográficas. Também é preciso conceder permissões sobre a tabela **spatial_ref_sys**, que possui os dados geográficos necessários para o funcionamento do SIG.

Após tudo acertado basta executar o seguinte comando para criar uma tabelas contendo os dados geográficos extraídos do shapefile:

<div style="font-family: monospace;">psql -d geo_bd_name -U geo_user -f arquivo.sql2</div>Para configurar o GeoServer siga os passos do [seguinte tutorial](http://docs.codehaus.org/display/GEOSDOC/PostGIS+DataStore).

Plugins para acesso a outras fontes de dados podem ser encontrados na [página na sourceforge](http://sourceforge.net/project/showfiles.php?group_id=25086&package_id=129885).

### ArcSDE como fonte de dados

O [ArcSDE](http://www.esri.com/software/arcgis/arcsde/about/overview.html) é um sistema proprietário desenvolvido pela ESRI que efetua a conexão entre o sistema ArcGIS e diversos SGBDs. O GeoServer pode ser configurado para utilizar o ArcSDE como fonte de dados de suas requisiçõs.

[Tutorial](http://docs.codehaus.org/display/GEOTDOC/ArcSDE+DataStore) de como utilizar o plugin para conexão com o ArcSDE (note que o plugin [não funciona](http://sourceforge.net/mailarchive/message.php?msg_id=c2a28b1c5d208c6a6933f00a21c496a3%40145.50.39.8) no GeoServer 1.6 RC2 ou RC3.

Lembre-se de baixar o pacote com o patch da ESRI ArcSDE e colocar os **todos** os arquivos *jar* necessários (é só ver o [tutorial](http://docs.codehaus.org/display/GEOTDOC/ArcSDE+DataStore)) no diretório <tt>$GEOSERVER_HOME/webapps/geoserver/WEB_INF/lib/</tt>.


## OpenLayers

Instalado o GeoServer é preciso pensar: *como* criar um aplicação PHP com ela? Ok, não é preciso pensar nisso, mas é o que estou me perguntando agora.

A interface com o usuário apresentada pelo GeoServer é baseada na biblioteca de [OpenLayers](http://www.openlayers.org/), que se trata de uma biblioteca **javascript***aberta e livre* para criação de sistemas semelhantes ao Google Maps ou ao MS Live Earth.

A configuração e personalização do openlayers exige bastante programação javascript, por isso recomendo a utilização do plugin do Eclipse **jseclipse**.


## Referências

- [mapserver-versus-geoserver](http://www.fernandoquadro.com.br/html/2007/07/18/mapserver-versus-geoserver/)
- [Wikipedia](http://pt.wikipedia.org/wiki/Sistema_de_Informa%C3%A7%C3%A3o_Geogr%C3%A1fica)
- **README** do postgresql-8.2-postgis – /usr/share/doc/postgresql-8.2-postgis/README.Debian.gz
- [Guia do usuário](http://docs.codehaus.org/display/GEOSDOC/User+Tutorial+Shapefile) do GeoServer
- [Guia do usuário](http://docs.codehaus.org/display/GEOTDOC) GeoServer


