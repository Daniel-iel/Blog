+++
author = "Daniel Oliveira"
title = "Simplificando o uso do namespace 💡"
date = "2022-08-08"
description = "C# Tip"
tags = [
    "c#10",
    "c#",
    "namespace",    
    "CleanCode"
]
+++

C# Tip 💡

Junto com o c# 10 vieram bastantes melhorias e uma delas é a possibilidade de usar o namespace do código de uma forma mais simplicita, melhorando a legibilidade do código.

## ❌

```csharp
namespace Exemplo
{
  class Program
  {
    static void Main(string[] args)
    {
      Console.WriteLine("Hello World!");
    }
  }
}
```

## ✔️

```csharp
namespace Exemplo;

class Program
{
  static void Main(string[] args)
  {
    Console.WriteLine("Hello World!");
  }
}
```
