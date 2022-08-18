+++
author = "Daniel Oliveira"
title = "Usando required keyword💡"
date = "2022-08-17"
description = "C# Tip"
tags = [
    "c# 11",
    "c#",
    "required keyword",
    "C# tips"   
]
+++

C# Tip 💡

C# 11 𝗿𝗲𝗾𝘂𝗶𝗿𝗲𝗱 keyword, permite que uma propriedade seja marcada com obrigatória, forçando o desenvolvedor a fornecer um valor para essa propriedade em tempo de desenvolvimento.

```csharp
public class Exemplo
{
    public required string Nome { get; init; }
    public string Sobrenome { get; init; }
}

var exemplo = new Exemplo()
{
    Sobrenome = "Sobrenome"
};
```

:memo: **Note:** o código `var exemplo = new Exemplo()` será marcado com erro pelo compilador.