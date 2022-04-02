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

Spinner é distribuído através do [nuget](https://www.nuget.org/packages/Spinner/), compátivel com **.net core 3, 3.1** e **.net 5 e 6**.

``` csharp
    Install-Package Spinner
```

## Configurar um objeto

Para configurar o layout da string que iremos gerar no final do processo, iremos utilizar os atributos `ObjectMapper` e `WriteProperty`.

**ObjectMapper:** é o atributo que trabalha como um limitado geral de posições, ou seja, se a string que estamos gerando for maior que o valor do atributo, o restante será ignorado.

- **length:** o tamanho maximo do string final.

**WriteProperty:** é o atributo que define a posição que iremos escrever o valor.

- **length:** o tamanho maximo do campo.
- **order:** a posição do campo dentro da string.
- **paddingChar:** o caracter que iremos utilizar para preencher o campo, caso o valor do campo não atinja o limite que estabelecemos no campo length.

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

## Usando o Spinner

``` csharp
    //instanciando a classe
    Pessoa pessoaEscrita = new Pessoa("Fulano", "011659888888");
    
    //instanciando o Spinner
    Spinner<Pessoa> spinner = new Spinner<Pessoa>(pessoaEscrita);

    //gerando a string
    string stringResponse = spinner.WriteAsString();

    //Resultado:               Fulano   011659888888

    //Convertendo a string para um objeto
    Spinner<Pessoa> spinnerReader = new Spinner<Pessoa>();
    Pessoa pessoaLeitor = spinnerReader.ReadFromString("               Fulano   011659888888");
```
