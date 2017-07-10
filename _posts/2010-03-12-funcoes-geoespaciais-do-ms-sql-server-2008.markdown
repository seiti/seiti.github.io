---
layout: post
title: Funções Geoespaciais do MS SQL Server 2008
date: '2010-03-12 18:24:28'
tags:
- arcgis
- geo
---


O MS SQL Server 2008 (MSSQL) possui um tipo próprio para guardar geometrias: [*geometry*](http://msdn.microsoft.com/en-us/library/cc280487.aspx) (tem um *geography* também, mais útil para representar feições mais extensas).

E ainda [ implementa](http://msdn.microsoft.com/en-us/library/bb933973.aspx) os métodos definidos pela OGC.

Isto possibilita operações CRUD sobre o dados georreferenciados, diretamente através de comandos SQL.

Os métodos estáticos, acessíveis através de <tt>geometry::NomeDoMétodo()</tt>,  são:

- [STGeomFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933823.aspx)
- [STPointFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933821.aspx)
- [STLineFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933839.aspx)
- [STPolyFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933922.aspx)
- [STMPointFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933833.aspx)
- [STMLineFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933836.aspx)
- [STMPolyFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933986.aspx)
- [STGeomCollFromText (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933818.aspx)
- [STGeomFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933882.aspx)
- [STPointFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933813.aspx)
- [STLineFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933980.aspx)
- [STPolyFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933907.aspx)
- [STMPointFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933801.aspx)
- [STMLineFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933800.aspx)
- [STMPolyFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933964.aspx)
- [STGeomCollFromWKB (geometry Data Type)](http://msdn.microsoft.com/en-us/library/bb933889.aspx)

E os métodos do objeto *geometry*:

- [STArea](http://msdn.microsoft.com/en-us/library/bb933923.aspx)
- [STAsBinary](http://msdn.microsoft.com/en-us/library/bb933881.aspx)
- [STAsText](http://msdn.microsoft.com/en-us/library/bb933977.aspx)
- [STBoundary](http://msdn.microsoft.com/en-us/library/bb933985.aspx)
- [STBuffer](http://msdn.microsoft.com/en-us/library/bb933963.aspx)
- [STCentroid](http://msdn.microsoft.com/en-us/library/bb933847.aspx)
- [STContains](http://msdn.microsoft.com/en-us/library/bb933904.aspx)
- [STConvexHull](http://msdn.microsoft.com/en-us/library/bb933878.aspx)
- [STCrosses](http://msdn.microsoft.com/en-us/library/bb933838.aspx)
- [STDifference](http://msdn.microsoft.com/en-us/library/bb933893.aspx)
- [STDimension](http://msdn.microsoft.com/en-us/library/bb933848.aspx)
- [STDisjoint](http://msdn.microsoft.com/en-us/library/bb933909.aspx)
- [STDistance](http://msdn.microsoft.com/en-us/library/bb933952.aspx)
- [STEndpoint](http://msdn.microsoft.com/en-us/library/bb933879.aspx)
- [STEnvelope](http://msdn.microsoft.com/en-us/library/bb933896.aspx)
- [STEquals](http://msdn.microsoft.com/en-us/library/bb933902.aspx)
- [STExteriorRing](http://msdn.microsoft.com/en-us/library/bb933955.aspx)
- [STGeometryN](http://msdn.microsoft.com/en-us/library/bb933831.aspx)
- [STGeometryType](http://msdn.microsoft.com/en-us/library/bb933825.aspx)
- [STInteriorRingN](http://msdn.microsoft.com/en-us/library/bb933843.aspx)
- [STIntersection](http://msdn.microsoft.com/en-us/library/bb933832.aspx)
- [STIntersects](http://msdn.microsoft.com/en-us/library/bb933899.aspx)
- [STIsClosed](http://msdn.microsoft.com/en-us/library/bb933815.aspx)
- [STIsEmpty](http://msdn.microsoft.com/en-us/library/bb933975.aspx)
- [STIsRing](http://msdn.microsoft.com/en-us/library/bb933982.aspx)
- [STIsSimple](http://msdn.microsoft.com/en-us/library/bb933974.aspx)
- [STIsValid](http://msdn.microsoft.com/en-us/library/bb933890.aspx)
- [STLength](http://msdn.microsoft.com/en-us/library/bb933978.aspx)
- [STNumGeometries](http://msdn.microsoft.com/en-us/library/bb933910.aspx)
- [STNumInteriorRing](http://msdn.microsoft.com/en-us/library/bb933845.aspx)
- [STNumPoints](http://msdn.microsoft.com/en-us/library/bb933916.aspx)
- [STOverlaps](http://msdn.microsoft.com/en-us/library/bb933817.aspx)
- [STPointN](http://msdn.microsoft.com/en-us/library/bb933908.aspx)
- [STPointOnSurface](http://msdn.microsoft.com/en-us/library/bb933826.aspx)
- [STRelate](http://msdn.microsoft.com/en-us/library/bb933915.aspx)
- [STSrid](http://msdn.microsoft.com/en-us/library/bb933851.aspx)
- [STStartPoint](http://msdn.microsoft.com/en-us/library/bb933804.aspx)
- [STSymDifference](http://msdn.microsoft.com/en-us/library/bb933820.aspx)
- [STTouches](http://msdn.microsoft.com/en-us/library/bb933953.aspx)
- [STUnion](http://msdn.microsoft.com/en-us/library/bb933850.aspx)
- [STWithin](http://msdn.microsoft.com/en-us/library/bb933991.aspx)
- [STX](http://msdn.microsoft.com/en-us/library/bb933828.aspx)
- [STY](http://msdn.microsoft.com/en-us/library/bb933990.aspx)

Estes métodos podem ser chamados da seguinte forma, por exemplo:

 SELECT coluna1.STArea() FROM tabela

onde <tt>coluna1</tt> é do tipo *geometry*.


