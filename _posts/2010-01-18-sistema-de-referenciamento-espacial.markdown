---
layout: post
title: Sistema de Referenciamento Espacial
date: '2010-01-18 17:19:09'
tags:
- geo
- gis
---


*Spatial Reference System*,  ou Sistema de Referenciamento Espacial, define como descrever uma posição, uma localização no espaço.

Para determinarmos essa posição precisamos de duas coisas: um ponto de referência e um sistema de coordenadas.


## *Datum*

Para descrever esta localização temos de levar em conta algumas coisas. Primeiro, a Terra não é plana. Verdade. E nem uma bola.  Mas podemos aproximar sua superfície à algumas formas geométricas.  A primeira que vem à mente é a **esfera**. É boa para se montar globos escolares e pintar os continentes em  bolas de  praia. Mas, como aprendemos na escolinha, a Terra é achatada nos pólos. Mas a aproximação com a esfera serve para qualquer coisa que conte com uma escala pequena.

<figure class="wp-caption aligncenter" style="width: 380px;">[![](http://upload.wikimedia.org/wikipedia/commons/9/9f/GEO_Globe.jpg)](http://pt.wikipedia.org/wiki/Ficheiro:GEO_Globe.jpg)<figcaption class="wp-caption-text">Globo terrestre</figcaption></figure>

Segue então uma segunda aproximação: um **elipsóide ou esferóide**. Ou uma esfera achatada.  Esta forma geométrica é bastante utilizada para descrever a superfície do planeta,  parte por facilitar bastante os cálculos envolvidos e parte por se adequar razoavelmente à superfície verdadeira da Terra. Para obter um grau maior de aproximação modificamos os tamanhos dos eixos do elipsóide e também deslocamos seu centro, ajeitando-o com relação à Terra.

Ou seja, se a Terra fosse um esferóide perfeito, todos os pontos de sua superfície iriam tocar nos pontos do esferóide de referência.  Como isso não ocorre, a gente ajeita o esferóide, *definindo em que pontos* o esferóide toca a superfície do planeta.  Note que definição de pontos tem *data de validade*, ou pelo menos data de referência, visto que a [posição relativa entre os continentes muda com o tempo](http://pt.wikipedia.org/wiki/Deriva_continental). Digamos que nosso esferóide toca a superfície do planeta em um ponto específico de Pindamonhangaba e em outro em Paris. Infelizmente estes pontos não corresponderão exatamente ao mesmo local no dia seguinte. Por isso temos nomes como WGS84, SAD69. Os números se referem ao ano .

<figure class="wp-caption aligncenter" style="width: 383px;">[![](http://upload.wikimedia.org/wikipedia/commons/b/b5/OblateSpheroid.PNG)](http://pt.wikipedia.org/wiki/Ficheiro:OblateSpheroid.PNG)<figcaption class="wp-caption-text">Esferóide</figcaption></figure>Uma outra forma é a **geóide**. A geóide se trata de uma figura geométrica cuja superfície possui sempre a mesma força gravitacional, correspondendo mais ou menos ao nível médio do mar. Uma esfera não rolaria para lado nenhum em cima da superfície de uma geóide. Os cálculos sobre esta figura são mais complicados, mas é uma aproximação bastante útil para analisar a construção de canais, rodovias extensas e redes de água e esgoto.

<figure class="wp-caption aligncenter" style="width: 490px;">[![](http://upload.wikimedia.org/wikipedia/commons/5/56/Geoids_sm.jpg)](http://pt.wikipedia.org/wiki/Ficheiro:Geoids_sm.jpg)<figcaption class="wp-caption-text">Geóide</figcaption></figure>A escolha da figura geométrica, a definição de suas dimensões e o posicionamento desta figura com relação à Terra nos dá o ***datum*** (nota: só estou considerando sistema geocêntricos, deixando os topocêntricos de lado).

<figure class="wp-caption aligncenter" style="width: 400px;">[![](http://upload.wikimedia.org/wikipedia/commons/8/86/Sperm-egg.jpg)](http://en.wikipedia.org/wiki/File:Sperm-egg.jpg)<figcaption class="wp-caption-text">Espermatozóide</figcaption></figure>
## Sistema Geográfico de Coordenadas

Temos um *datum*. Mas isto não basta. Precisamos de um sistema de coordenadas para localizar o que quer que seja. Para isto temos um Sistema Geográfico de Coordenadas (*geographic coordinate system* ou **GCS**), também conhecido como sistema **esférico** de coordenadas,  que inclui uma unidade de medida angular, um meridiano principal e um *datum*.

<figure class="wp-caption aligncenter" style="width: 320px;">[![](http://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Geographic_coordinates_sphere.svg/500px-Geographic_coordinates_sphere.svg.png)](http://en.wikipedia.org/wiki/File:Geographic_coordinates_sphere.svg)<figcaption class="wp-caption-text">Latitude (φ) e Longitude (λ)</figcaption></figure>Com o *datum*, o equador e o meridiano principal, geralmente o de *Greenwich*, conseguimos um ponto de referência,  onde φ = 0° e λ = 0°,  e o centro do esferóide, a partir do qual todas as medidas são baseadas. Só para constar, a cidade de São Paulo se encontra em <tt>23°33′0″ S, 46°38′0″ W</tt>, ou seja, latitude  <tt>-23°33′0″</tt> e longitude<tt> -46°38′0″</tt>.


## Sistema de Coordenadas Projetadas

O GCS ajuda a localizar algum ponto. Mas para visualizar o mapa no papel, ou na tela do computador, precisamos levar tudo que está em um objeto 3D em pontos correspondentes em um plano 2D. Isto se chama **projeção**. A mesma projeção que se ensina nas aulas de matemática da escolinha, mas [aplicada em nossos mapas](http://en.wikipedia.org/wiki/Map_projection).

Pensando na superfície da Terra, podemos pensar em algumas características:

- Área
- Forma
- Direção
- Posicionamento relativo
- Distância
- Escala

Quando projetamos esta superfície em um plano, podemos preservar algumas delas. Mas não todas. Por isto existem vários tipos de projeção. Cada uma prioriza alguma das propriedades descritas. A mais famosa é a Projeção de Mercator, que privilegia direção e posicionamento relativo.

<figure class="wp-caption aligncenter" style="width: 464px;">[![](http://upload.wikimedia.org/wikipedia/commons/thumb/7/74/Mercator-projection.jpg/773px-Mercator-projection.jpg)](http://en.wikipedia.org/wiki/File:Mercator-projection.jpg)<figcaption class="wp-caption-text">Projeção de Mercator</figcaption></figure>A projeção de Mercator é do tipo cilíndrica. Pense em uma bola de tênis enfiada em uma lata de batatas Pringles.  O problema dela é que deforma bastante a área conforme nos afastamos da linha do Equador. É só reparar no tamanho da Ántártica, que não é nem o dobro da do Brasil.

O cilindro em que é projetado o mapa tem seu eixo na mesma direção do eixo de rotação da Terra,  ou seja, o cilindro toca a Terra ao longo da linha do Equador.

<figure class="wp-caption aligncenter" style="width: 265px;">[![](http://webhelp.esri.com/arcgisdesktop/9.2/published_images/lightbulb.gif)](http://webhelp.esri.com/arcgisdesktop/9.2/index.cfm?TopicName=About_map_projections)<figcaption class="wp-caption-text">Projeção cilíndrica</figcaption></figure>

Isto nos leva à outra projeção importante: o Sistema Universal Transverso de Mercator (**UTM**). Ele é bastante semelhante à projeção de Mercator tradicional.

As diferenças são que o eixo do cilindro faz 90° com o eixo de rotação da Terra e o próprio cilindro é rotacionado  para obtermos projeções  mais precisas em cada fatia em que o cilindro toca a Terra.

<figure class="wp-caption aligncenter" id="attachment_941" style="width: 531px;">[![](http://seiti.eti.br/blog/wp-content/uploads/2010/01/projections.parsys.19330.Image_.gif "projections.parsys.19330.Image")](http://www.swisstopo.admin.ch/internet/swisstopo/en/home/topics/survey/sys/refsys/projections.html)<figcaption class="wp-caption-text">Universal Transverse of Mercator</figcaption></figure>Estas fatias são então quadriculadas em uma grade. Cada quadrado desta grade forma então um sistema de coordenadas cartesianas, onde a unidade de medida é o **metro**.


## Sistema de Referenciamento Espacial (Spatial Reference System)

E por fim temos o sistema de referencimento espacial, que nada mais é que a descrição de um conjunto que tem tudo que esta aí em cima. Um exemplo:

 GEOGCS["SAD69", DATUM["South_American_Datum_1969", SPHEROID["GRS 1967 (SAD69)",6378160,298.25, AUTHORITY["EPSG","7050"]], AUTHORITY["EPSG","6618"]], PRIMEM["Greenwich",0, AUTHORITY["EPSG","8901"]], UNIT["degree",0.01745329251994328, AUTHORITY["EPSG","9122"]], AUTHORITY["EPSG","4618"]]

O que é descrito acima, num formato conhecido como *Well Known Text* (WKT),  é o sistema SAD 69. Note é descrito o sistema geográfico de coordenadas (**GEOGCS**) com o *datum* utilizado,  o meridiano principal – Greenwich e a unidade de medida – *degree*,  assim como outras informações.  É comum utilizar apenas um número para nos referir a esta referência espacial. Este número, o [SRID](http://en.wikipedia.org/wiki/SRID),  pode ser visto na última linha: **EPSG 4618.** Muito mais exemplos em [SpatialReference.org](http://www.spatialreference.org/).

Outro exemplo:

 PROJCS["SIRGAS 2000 / UTM zone 23S", GEOGCS["SIRGAS 2000", DATUM["Sistema_de_Referencia_Geocentrico_para_America_del_Sur_2000", SPHEROID["GRS 1980",6378137,298.257222101, AUTHORITY["EPSG","7019"]], TOWGS84[0,0,0,0,0,0,0], AUTHORITY["EPSG","6674"]], PRIMEM["Greenwich",0, AUTHORITY["EPSG","8901"]], UNIT["degree",0.01745329251994328, AUTHORITY["EPSG","9122"]], AUTHORITY["EPSG","4674"]], UNIT["metre",1, AUTHORITY["EPSG","9001"]], PROJECTION["Transverse_Mercator"], PARAMETER["latitude_of_origin",0], PARAMETER["central_meridian",-45], PARAMETER["scale_factor",0.9996], PARAMETER["false_easting",500000], PARAMETER["false_northing",10000000], AUTHORITY["EPSG","31983"], AXIS["Easting",EAST], AXIS["Northing",NORTH]]

Neste caso é descrito um sistema de coordenadas projetadas (**PROJCS**), o que requer, além das informações previstas para o GEOGCS, qual o tipo de projeção – *Transverse Mercator* – e localização do ponto de referência  que determina o origem do sistema de medidas, no caso  em metros.  O srid é **31983.**

Ao invés de passar toda estas informações para alguém, basta informar o SRID.  Finalmente sabemos de onde vem o tal SRID que popula nossos banco de dados geográficos, e que devemos passar como parâmetro para as APIs Geo deste  mundão esferóide afora.


