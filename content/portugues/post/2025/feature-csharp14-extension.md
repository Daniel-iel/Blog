+++
author = "Daniel Oliveira"
title = "Nova Feature C# 14 (extension)💡"
date = "2025-05-16"
description = "C# Tip"
tags = [
    "c#14",
    "c#",
    "extension",    
]
+++

Antes da versão 14 do C#, para criar um método de extensão era necessário definir uma classe estática e utilizar o modificador `this` no primeiro parâmetro. Um dos problemas dessa abordagem era que esses arquivos costumavam crescer desorganizadamente, acumulando métodos com finalidades diversas.

Com a nova versão, a sintaxe foi simplificada, permitindo declarar métodos de extensão diretamente dentro de um escopo mais organizado, como `extension<string>(IEnumerable<string> source)`, o que torna o código mais limpo e modular.

A versão 14 do C# está prevista para ser lançada em novembro de 2025.

*Antes da versão C# 14*

```csharp
public static class Enumerable
{ 
    public static string Find(this IEnumerable<string> source, Func<string, bool> predicate)
    {     
        ... 
    }

    public static string FindByName(this IEnumerable<string> source, Func<string, bool> predicate)
    {     
        ... 
    }
}
```

*Depois da versão C# 14*

```csharp
public static class Enumerable
{ 
    extension<string>(IEnumerable<string> source)
    {     
        public IEnumerable<string> Find(Func<string, bool> predicate) { ... }
        public IEnumerable<string> FindByName(Func<string, bool> predicate) { ... }
    }
}
```
