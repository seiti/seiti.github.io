---
layout: post
title: Estendendo o BoundField
date: '2007-11-13 19:38:22'
tags:
- aspnet
---


Uma das facilidades que o esquema POO provê é a criação de classes a partir de outras existentes, a fim de incorporarmos (ou até restringirmos) funcionalidades, através da *herança*.

No Asp.Net temos os controles GridView e DetailsView, muito úteis por simplificar o processo de listar e editar entradas em um banco de dados, por exemplo. Nelas temos os controles de campo, ou coluna, tais como o BoundField, ButtonField e TemplateField entre [outros](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.detailsview%28VS.80%29.aspx)<span></span>.

Se você já é familiar à utilização destes controles, sabe como eles acabam por ser limitados. Caso seja necessário uma simples validação em um campo no DetaisView é preciso substituir o BoundField por um TemplateField, e colocar em seu interior algo como um TextBox mais um RequiredFieldValidator ou algum outro controle de validação.

Pegue um formulário com uns 30 campos e verá o tamanho do trabalho braçal necessário para modificar o DetailsView. Se o lema da MS é criar sistemas sem perder tempo escrevendo linhas de código redundantes, espero também não perder este tempo substituindo tags no código.

Aí que entra a herança, podemos facilmente estender um BoundField e incorporar nele um validador como o RequiredFieldValidator. Assim podemos marcar nosso campo como obrigatório apenas marcando um atributo da tag como <tt>true</tt>.

Por exemplo, estendendo o BoundField em uma classe denominada MyBoundField e adicionando uma propriedade denominada **RequiredField** podemos substituir a tag:

<div style="font-family: monospace;"><boundfield datafield="<span">“numCNPJ” HeaderText=<span>“CNPJ”</span> SortExpression=<span>“numCNPJ”</span> /></boundfield></div>Por:

<div style="font-family: monospace;"><myboundfield datafield="<span">“numCNPJ” HeaderText=<span>“CNPJ”</span> SortExpression=<span>“numCNPJ”</span> RequiredField=<span>“true”</span> /></myboundfield></div>Ao invés da prolixa:

<div style="font-family: monospace;"><templatefield headertext="<span">“CNAE” SortExpression=<span>“numCNPJ”</span>>  
<edititemtemplate>  
<textbox id="<span">“TextBox1” runat=<span>“server”</span> Text=<span>‘’></span></textbox>  
<requiredfieldvalidator id="<span">“RequiredFieldValidator1” runat=<span>“server”</span> ControlToValidate=<span>“TextBox1”</span> ErrorMessage=<span>“Campo requerido!”</span> />  
</requiredfieldvalidator></edititemtemplate>  
<insertitemtemplate>  
<textbox id="<span">“TextBox2” runat=<span>“server”</span> Text=<span>‘’></span></textbox>  
<requiredfieldvalidator id="<span">“RequiredFieldValidator2” runat=<span>“server”</span> ControlToValidate=<span>“TextBox2”</span> ErrorMessage=<span>“Campo requerido!”</span> />  
</requiredfieldvalidator></insertitemtemplate>  
<itemtemplate>  
<label id="<span">“Label1” runat=<span>“server”</span> Text=<span>‘’></span></label>  
</itemtemplate>  
</templatefield></div>O código da classe MyBoundField é o seguinte:

 using System; using System.Collections.Generic; using System.Text; using System.Data; using System.Configuration; using System.Web; using System.Web.Security; using System.Web.UI; using System.Web.UI.WebControls; using System.Web.UI.WebControls.WebParts; using System.Web.UI.HtmlControls; using System.ComponentModel; namespace Custom.DataBinding { /// <summary> /// A custom BoundField that agregates validators /// </summary> public class MyBoundField : System.Web.UI.WebControls.BoundField { protected override void InitializeDataCell(DataControlFieldCell cell, DataControlRowState rowState) { base.InitializeDataCell(cell, rowState); if (this.RequiredField) { if (cell.Controls[0] is TextBox) { TextBox box = cell.Controls[0] as TextBox; box.ID = this.DataField; } RequiredFieldValidator reqField = new RequiredFieldValidator(); reqField.ControlToValidate = this.DataField; reqField.Text = "*"; reqField.ErrorMessage = this.HeaderText + " is required."; reqField.Display = ValidatorDisplay.Dynamic; cell.Controls.Add(reqField); } } /// <summary> /// Require Validation /// </summary> /// [Browsable(true)] public bool RequiredField { get { if (ViewState["RequiredField"] == null) return false; return (bool)ViewState["RequiredField"]; } set { ViewState["RequiredField"] = value; } } } }

Para utilizá-la em sua solução, basta criar um projeto que contenha a classe acima e colocar a diretiva <tt>Register</tt> na página aspx ou ascx:

<div style="font-family: monospace;"><span>@ Register Assembly=<span>“NomeDoAssembly”</span> Namespace=<span>“Custom.DataBinding”</span> TagPrefix=<span>“cc1”</span><span>%></span></span></div>Ou seu equivalente no <tt>Web.config</tt>.

**Nota**: Infelizmente parece que o autocompletar do intellisense não funciona ao utilizar o [MyBoundField](../../wiki/MyBoundField/edit "Create this page"), limitando bastante os prós deste tipo de abordagem. Verificarei com mais cuidado o porquê disto. Tem alguma informação aqui: [intellisense in html view](http://forums.asp.net/t/1076608.aspx?PageIndex=1). O caso é que se for necessário criar um XSD contendo a definição do novo controle, será muito difícil utilizar estas classes estendidas durante o desenvolvimento.


