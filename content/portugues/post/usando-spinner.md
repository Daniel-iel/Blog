+++
author = "Daniel Oliveira"
title = "Usando Spinner"
date = "2022-04-02"
description = "Como usar o Spinner em .net."
tags = [
    "spinner",
    "string-posicional",
    ".net"
]
+++

Spinner é um mapeador de objetos simples, útil para se comunicar com qualquer sistema que use uma string posicional como comunicação.

## Instalação

Spinner é distribuído através do [nuget](https://www.nuget.org/packages/Spinner/), compatível com **.net core 3, 3.1** e **.net 5 e 6**.

``` csharp
    Install-Package Spinner
```

## Configurando um objeto

Para configurar o layout da string que iremos gerar no final do processo, iremos utilizar os atributos `ObjectMapper` e `WriteProperty`.

**ObjectMapper:** atributo que trabalha como um limitado geral de posições, ou seja, se a string que estamos gerando for maior
que a soma de todos os valores contidos na propriedade *length* dos atributos **WriteProperty** e **ReadProperty**, os caracteres que excederem o limite serão ignorados.

- **length:** tamanho máximo da string final.

**WriteProperty:** atributo que define a posição que iremos escrever o valor.

- **length:** tamanho máximo do campo.
- **order:**  posição do campo na string.
- **paddingChar:** caractere que iremos utilizar para preencher o campo, caso o valor do campo não atinja o limite que estabelecemos no campo length.

``` csharp
[ObjectMapper(length: 35)]
public struct Pessoa
{
    public Pessoa(string nome, string telefone)
    {
        this.Nome = nome;
        this.Telefone = telefone;
    }

    [WriteProperty(length: 20, order: 1, paddingChar: ' ')]
    public string Nome { get; private set; }

    [WriteProperty(length: 15, order: 2, paddingChar: ' ')]
    public string Telefone { get; private set; }
}
```

**ReadProperty:** atributo que define a posição que iremos escrever o valor.

- **start:** posição inicial do campo dentro da string.
- **length:** tamanho de caracteres do campo.
  
``` csharp
[ObjectMapper(length: 35)]
public struct Pessoa
{
    public Pessoa(string nome, string telefone)
    {
        this.Nome = nome;
        this.Telefone = telefone;
    }

    [ReadProperty(start: 0, length: 19 )]     
    public string Nome { get; private set; }

    [ReadProperty(start: 20, length: 15 )]
    public string Telefone { get; private set; }
}
```

## Usando o Spinner

Podemos usar o spinner de duas formas, a primeira é convertendo uma instância de um objeto em string, e a segunda é convertendo uma string em um objeto.

### Escrevendo uma string

``` csharp
    //instanciando a classe
    Pessoa pessoa = new Pessoa("Fulano", "011659888888");    
    //instanciando o Spinner
    Spinner<Pessoa> spinner = new Spinner<Pessoa>(pessoa);
    //gerando a string
    string stringGerada = spinner.WriteAsString();
    //stringGerada:               Fulano   011659888888
```

### Lendo uma string

``` csharp
    //Convertendo a string em um objeto
    Spinner<Pessoa> spinnerReader = new Spinner<Pessoa>();
    Pessoa pessoa = spinnerReader.ReadFromString("               Fulano   011659888888");
```

:memo: **Note:** Ao gerar a string, um contrato deve ser estabelecido entre às partes que irão se comunicar, pois, qualquer ruído nesse contrato estabelecido, pode gerar uma leitura da string errada causando perda de informação.

Como pudemos ver neste artigo, spinner é um framework simples, porém muito útil facilitando a escrita e leitura de strings.
Para mais informações sobre o Spinner, acesse o [repositório](https://github.com/SpinnerAlloc/Spinner) e a [documentação](https://spinnerframework.com/).
