+++
author = "Daniel Oliveira"
title = "Using Spinner"
date = "2022-05-28"
description = "How use Spinner in .net."
tags = [
    "spinner",
    "string-posicional",
    ".net"
]
+++

Spinner is a simple object mapper, useful for communicating with any system that uses a positional string as communication.

## Instalation

Spinner is distributed through the [nuget](https://www.nuget.org/packages/Spinner/), compatible with **.net core 3, 3.1** e **.net 5 e 6**.

``` csharp
    Install-Package Spinner
```

## Configuring an object

To configure the layout of the string that we will generate at the end of the process, we will use the `ObjectMapper` and `WriteProperty` attributes.

**ObjectMapper:** attribute that works as a general bound of positions, that is, if the string we are generating is longer than the sum of all values ​​contained in the *length* property of the **WriteProperty** and **ReadProperty** attributes, characters that exceed the limit will be ignored.

- **length:** maximum length of the final string.

**WriteProperty:** attribute that defines the position where we will write the value.

- **length:** maximum field length.
- **order:** field position in the string.
- **paddingChar:** character that we will use to fill the field, in case the value of the field does not reach the limit that we established in the field length.

``` csharp
[ObjectMapper(length: 35)]
public struct Person
{
    public Person(string name, string phone)
    {
        this.Name = name;
        this.Phone = phone;
    }

    [WriteProperty(length: 20, order: 1, paddingChar: ' ')]
    public string Name { get; private set; }

    [WriteProperty(length: 15, order: 2, paddingChar: ' ')]
    public string Phone { get; private set; }
}
```

**ReadProperty:** attribute that defines the position where we will write the value.

- **start:** starting position of the field within the string.
- **length:** field character length.
  
``` csharp
[ObjectMapper(length: 35)]
public struct Person
{
    public Person(string name, string phone)
    {
        this.Name = nome;
        this.Phone = phone;
    }

    [ReadProperty(start: 0, length: 19 )]     
    public string Name { get; private set; }

    [ReadProperty(start: 20, length: 15 )]
    public string Phone { get; private set; }
}
```

## Using Spinner

We can use the spinner in two ways, the first is by converting an instance of an object to a string, and the second is by converting a string into an object.

### Writing a string

``` csharp
    //instanciate a class
    Person person = new Person("Fulano", "011659888888");    
    //instanciate the Spinner
    Spinner<Person> spinner = new Spinner<Person>(person);
    //generate a string
    string positionalString = spinner.WriteAsString();
    //string:               Fulano   011659888888
```

### Reading a string

``` csharp
    //Converting the string to an object
    Spinner<Person> spinnerReader = new Spinner<Person>();
    Person person = spinnerReader.ReadFromString("               Fulano   011659888888");
```

:memo: **Note:** When generating the string, a contract must be established between the parties that will communicate, because any noise in this established contract can generate a reading of the wrong string causing loss of information.

As we could see in this article, spinner is a simple but very useful framework facilitating the writing and reading of strings.
For more information about Spinner, visit [repository](https://github.com/SpinnerAlloc/Spinner) and [documentation](https://spinnerframework.com/).
