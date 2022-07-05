+++
author = "Daniel Oliveira"
title = "Usando Code Snippet no visual studio 2022"
date = "2022-04-02"
description = "Como usar o Spinner em .net."
tags = [
    "Atalho de código",
    "Code Snippets",
    "Dotnet",
    "Produtividade"
]
+++

Code Snippet é uma forma encapsular trechos de código em forma de atalhos, podendo ser usado em qualquer parte do sistema, melhorando a produtividade do desenvolvedor.

:memo: **Note:** Para os exemplos aqui usados, o código foi pensado usando o visual studio 2022, pode haver diferenças nas versões anteriores ou posteriores.

## Entendendo a estrututa

````xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title></Title>
      <Author></Author>
      <Description></Description>
      <Shortcut></Shortcut>
    </Header>
    <Snippet>
      <Code Language="CSharp">
        <![CDATA[         
        ]]>
      </Code>
      <Declarations>
        <Literal>
          <ID></ID>          
          <Default></Default>
          <ToolTip></ToolTip>
        </Literal>       
      </Declarations>      
      <Imports>
        <Import>
          <Namespace></Namespace>
        </Import>
      </Imports>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
````

### Header

 A tag header contém informações sobre o code snippet, os campos description e title irão aparecer no visual studio ao digitar o atalho do código.

- **Title**: título do código snippet.
- **Author**: autor do código snippet.
- **Description**: descrição do código snippet.
- **Shortcut**: atalho do código snippet.

### Code

 A tag code é utilizada para definir o código que será executado, quando o atalho do campo Shortcut for digitado na linguqgem escolhida.

### Literal

A tag literal é utilizada para definir o valor que será substituído no código.

- **ID**: nome do parâmetro que será substituído no código.
- **Default**: valor padrão do parâmetro.
- **ToolTip**: texto que será exibido no tooltip do parâmetro.

### Imports

A tag import é utilizada para importar bibliotecas que serão utilizadas no código.

- **Namespace**: se o seu código necessitar de algum using, o namespace deve ser definido nessa tag.

## Exemplo

Para o nosso exemplo, vamos criar um código snippet que irá criar um range de números e com o resultado, iremos exibir o total de números gerados.

### Criando um arquivo

Salve o xml abaixo de exemplo `{NOME_ARAQUIVO}.snippet` em algum diretório seu computador que você possa acessar.

````xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>Exemplo</Title>
      <Author>Daniel Oliveira</Author>
      <Description>Código facilidador para instanciar o spinner.</Description>
      <Shortcut>example</Shortcut>
    </Header>
    <Snippet>
      <Code Language="CSharp">
        <![CDATA[
            var $NomeVariavel$ = Enumerable.Range(1, 10);
            Console.WriteLine("Total: " + $NomeVariavel$.Count());
        ]]>
      </Code>
      <Declarations>
        <Literal>
          <ID>NomeVariavel</ID>          
          <Default>nome_variavel</Default>
          <ToolTip>Nome da variável do range.</ToolTip>
        </Literal>        
      </Declarations>      
      <Imports>
        <Import>
          <Namespace>System.Linq</Namespace>
        </Import>
      </Imports>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
````

:memo: **Note:** É importante que o arquivo xml tenha a extensão .snippet.

### Importando o arquivo

1. Abra o visual studio.
2. Localize a barra de ferramentas no menu superior.
3. Digite `Code Snippet manger`.
4. No dropdown de opções, selecione a linguagem do código e clique na opção importar.
5. Localize o arquivo salvo no computador e depois clique em finalizar.
6. Abra um arquivo na liguagem selecionado na tag Code do arquivo .snippet, digite o atalho do código + tab + tab para ver o resultado.

![ ](/Blog/images/posts/code-snippet.gif)

## Referências

<https://docs.microsoft.com/en-us/visualstudio/ide/walkthrough-creating-a-code-snippet?view=vs-2022>
