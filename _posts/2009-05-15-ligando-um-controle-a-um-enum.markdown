---
layout: post
title: Ligando um controle à um Enum
date: '2009-05-15 09:50:47'
tags:
- aspnet
---


As **enumerações**, ou simplesmente [enums](http://en.wikipedia.org/wiki/Enumerated_type), são comumentes usados para substituir [valores mágicos](http://en.wikipedia.org/wiki/Magic_number_%28programming%29) e deixando o código mais legível e auto-documentado.

Mas em Asp.NET, às vezes se torna necessário listar os “valores” de um enum. “Valores” está entre aspas porque não é necessariamente o valor que a gente quer ligar, pois [este valor é um número inteiro](http://msdn.microsoft.com/pt-br/library/sbbt4032(VS.80).aspx).

public enum CMYK { CYAN, MAGENTA, YELLOW, KEY }

No caso, *CYAN = 0, MAGENTA = 1* e daí em diante. Seria legal então podermos [ligar (através do DataSource/DataBind) este nosso enum em um controle](http://geekswithblogs.net/jawad/archive/2005/06/24/EnumDropDown.aspx), por exemplo um *DropDownList*, que deve apresentar CYAN, MAGENTA, YELLOW e KEY como opções.

protected System.Web.UI.WebControls.DropDownList ddColorComponent; private void Page_Load(object sender, System.EventArgs e) { if(!IsPostBack) { ddColorComponent.DataSource = Enum.GetNames(typeof(CMYK)); ddColorComponent.DataBind(); } } private void ddColorComponent_SelectedIndexChanged(object sender, System.EventArgs e) { Color selectedColor = (Color)Enum.Parse(ddColorComponent.SelectedValue); }

Podemos [melhorar isto](http://developcode.blogspot.com/2006/12/dropdownlists-with-enums-as-datasource.html) e dar nomes mais descritivos aos nossos enums através de atributos:

using System.ComponentModel; public enum CMYK { [Description("Ciano")] CYAN, [Description("Magenta")] MAGENTA, [Description("Amarelo")] YELLOW, [Description("Preto")] KEY }

Nesta solução, no entanto, devemos escrever o código que fornece uma lista de elementos para ser usada como DataSource. Primeiro devemos extrair o conteúdo inserido como atributo do enum através de *reflection*:

using System.ComponentModel; using System.Reflection; ... ... public static string GetDescription(Enum value) { FieldInfo fieldInfo = value.GetType().GetField(value.ToString()); DescriptionAttribute[] attributes = (DescriptionAttribute[])fieldInfo.GetCustomAttributes(typeof(DescriptionAttribute), false); return (attributes.Length > 0) ? attributes[0].Description : value.ToString(); }

Assim é possível iterar por todos os itens do enum, criando uma lista:

public static List> GetValuesAndDescription(System.Type enumType) { List> kvPairList = new List>(); foreach (Enum enumValue in Enum.GetValues(enumType)) { kvPairList.Add(new KeyValuePair(enumValue.ToString(), GetDescription(enumValue))); } return kvPairList; }

O *DataBind* fica assim:

ddColorComponent.DataSource = EnumDescription.GetValuesAndDescription(typeof(CMYK)); ddColorComponent.DataTextField = "Value"; ddColorComponent.DataValueField = "Key";

Fonte: [http://developcode.blogspot.com/2006/12/dropdownlists-with-enums-as-datasource.html](http://developcode.blogspot.com/2006/12/dropdownlists-with-enums-as-datasource.html)


