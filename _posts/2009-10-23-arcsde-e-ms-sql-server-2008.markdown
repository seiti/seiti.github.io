---
layout: post
title: ArcSDE e MS SQL Server 2008
date: '2009-10-23 15:32:09'
tags:
- geo
- gis
---


O [**ArcSDE**](http://www.esri.com/software/arcgis/arcsde/)é um produto da **ESRI** que consiste-se em uma camada sobre bancos de dados relacionais, tornando-os capazes, se já não forem, de manipular informações geograficamente referenciadas, ou dados *geo*.

O MS SQL Server 2008 é o banco de dados relacionais da Microsoft.

A versão mais recente do ArcSDE, a 9.3, tornou possível utilizar o tipo de geometria nativa: o ‘GEOMETRY’ . Mas como configurar o sistema de forma a utilizá-lo?

Existe uma entrada no banco de dados que deve ser alterada. Ela se encontra na tabela **sde.db_tune**. Dê uma xeretada para verifcar seu conteúdo:

 SELECT * FROM sde.dbtune WHERE keyword like 'DEFAULTS'    AND parameter_name like 'GEOMETRY_STORAGE'

A entrada que deve ser alterada é esta:

 UPDATE sde.dbtune SET config_string = 'GEOMETRY' WHERE keyword like 'DEFAULTS' AND parameter_name like 'GEOMETRY_STORAGE'

A listagem de tipos disponíneis em seus respectivos sistema pode ser obtido no [help do ArcSDE](http://webhelp.esri.com/arcgisdesktop/9.3/index.cfm?TopicName=An_overview_of_feature_geometry_and_raster_data_storage).


