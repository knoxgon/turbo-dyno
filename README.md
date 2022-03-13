# TurboDyno
[![NuGet Version](https://img.shields.io/nuget/v/Knoxgon.TurboDyno.svg?style=flat-square)](https://www.nuget.org/packages/Knoxgon.TurboDyno/)
[![Issues](https://img.shields.io/github/issues/knoxgon/TurboDyno)](https://github.com/knoxgon/TurboDyno/issues)


TurboDyno, turbo, clax, dynamic property maker and mapper using Reflection
## Authors
__Volkan Güven ® KnoxGoN - 2022__

[![@Linkedin](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/volkan-g%C3%BCven-108883133)
[![@GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=whit)](https://github.com/knoxgon)

# Introduction
This project is created to help users refer the documentation of [TurboDyno](https://www.nuget.org/packages/Knoxgon.TurboDyno/)..

API, methods declaration, and its signatures are described with details.

# Motive
When one needs to create a class with dynamic properties, it shouldn't be hard to do it. Unfortunately, there isn't an easy way to pull it off.

I've created this library as a hobby project to help with my work duties. With this library, you could create a whole new class by either passing arbitrary number of properties or passing a huge class with properties, map it, create a new instance of it and even keep the property record of the created class at runtime.

Since this project is created in a relatively short time (ca 6 hours), I haven't had time to create support for nested object properties and custom object types. But don't worry! It's on the way!

# Requirements

## Supported frameworks

[![@Windows](https://img.shields.io/badge/.NET-5C2D91?style=for-the-badge&logo=.net&logoColor=white)](https://dotnet.microsoft.com/en-us/download)

- .NET 5.0
- .NET Standard 2.0
- .NET Framework 4.8
- .NET Framework 4.7.2


- ...More on the way


## Installation

Package manager installation

```ps
Install-Package Knoxgon.TurboDyno -Version 5.1.0.2

```

## Version History
- 5.1.0.2

        Bugfix: Erroneous value returned from from the passed token on DynoPropertyValues
- 5.1.0.1
        
        Added support for .NET 5.0, .Net Framework 4.8 and 4.7.2
- 5.1.0
        
        Stabilized and fully tested. It is now in Beta-phase.

- 5.0.0 *Deprecated*
- 4.4.5.5 *Deprecated*
- 4.4.5.4 *Deprecated*
- 4.4.5.3 *Deprecated*
- 4.4.5 *Deprecated*
- 4.4.5 *Deprecated*
- 4.4.1.2 *Deprecated*
- 4.3.5.3 *Deprecated*
- 4.3.5.2 *Deprecated*
- 4.3.0 *Deprecated*
- 4.2.0 *Deprecated*
- 4.1.5 *Deprecated*
- 4.1.10 *Deprecated*
- 2.2.3.25 *Deprecated*
- 2.1.5.10 *Deprecated*
- 1.0.0 *Deprecated*



# Supported property types

* bool
* decimal
* float
* double
* long
* ulong
* int
* uint
* short
* ushort
* DateTime
* DateTime?
* byte
* nint
* nuint
* sbyte
* char


## Example usage

In the following list, you'll see different usages of Clax.

Clax is the TurboDyno facility class to be able to use necessary functions. Core methods reside within Clax.

1. The first example lets you map, copy and return a dynamic type of __PersonRecord__. It solely copies properties from the provided generic type.

```csharp
using System;
using Knoxgon.TurboDyno;

public class PersonRecord
{
    public long Id { get; set; }
    public string Name { get; set; }
    public DateTime BirthDate { get; set; }
    public bool Status { get; set; }
}

void static main()
{
    //Creates new class from PersonRecord's properties.
    Type dynamicPersonType = Clax.Create<PersonRecord>(className: "MyDynamicPersonClass");

    //Gets the list of property info for each created dynamic property
    IEnumerable<Reflection.PropertyInfo> dynamicPersonProperties = dynamicPersonObject.GetDynoProperties();
    
    //Creates and returns a newly created list of the object type.
    //Kind of like -> var list = new List<int>();
    List<object> dynamicPersonObjectList = dynamicPersonType.NewList();
    
    //Returns the created property names.
    var dynamicPersonPropertyNames = Clax.GetPropertyNames();
}

```

2. __Let's create an arbitrary number of properties by passing a property list this time.__

```csharp
void static main()
{
    //For the simplest example, let's pass 2 runtime properties
    //NOTE that any property from any class can easily be mapped using the same method.
    
    //Properties: string: RepoId, bool: Active
    var listOfProps = ...;
    
    Type dynamicPersonType = Clax.Create(listOfProps, className: "MyDynamicPersonClass");

    //Gets the list of property info for each created dynamic property
    //You'll get RepoId and Active
    IEnumerable<Reflection.PropertyInfo> dynamicPersonProperties = dynamicPersonObject.GetDynoProperties();
    
    //A list instance of the new generated class type with RepoId and Active as members.
    List<object> dynamicPersonObjectList = dynamicPersonType.NewList();
    
    //Returns the created property names.
    var dynamicPersonPropertyNames = Clax.GetPropertyNames();
}
```

## Clax Function API

| Name  | Parameters |Returns| Description|
| ------------- |-------------|--------|--------------|
| Create        | IEnumerable\<PropertyInfo\> properties<br/>string className<br/> string optionalNamespace<br/>params string[] libraries| Type | Builds and creates a dynamic class with passed properties. Properties can be created, mapped and passed by the user. |
| Create\<T>    | string className<br/>string optionalNamespace<br/>params string[] libraries     |Type| Builds and creates a dynamic class from the provided generic class T. Properties are assigned with getter and setter.|
| GetPropertyNames      | |List\<string\>| A list of property names of the original passed type.|

## DynoExtensions Function API

| Name | Extension | Parameters |Returns| Description|
| ------------- |:--------:|-------------|--------|--------------|
|ToDynoList\<T\>| T || List\<T\> | Converts created type object to a list ||
|GetDynoProperties\<T\>| Type | | Converts created type object to a list |Gets the list of object properties|
|DynoPropertyValues | List\<object\> ||IEnumerable\<object\>| Returns a list of values of each property in a dyno list|
|DynoPropertyValues\<T\>|List\<T\>||IEnumerable\<object\>|Returns a list of values of each property in a generic dyno list|
|DynoPropertyValues\<object\>|List\<object\>|string propertyName,<br/> string token,<br/>DynoFilterAction action|IEnumerable\<object\> |Returns a filtered list of values of each property in a dyno list with a single name predicate. <br/>This specific method allows to keep or remove the provided string token from the start of the value from the targeted property|
|DynoPropertyNames|List\<object\>||IEnumerable\<string\>|Returns a list of property names for each object in the passed dyno list
| New    | object ||object | Creates and returns a dyno instance of your object. Type is auto fetched from the object.|
| New      | Type ||object| Creates and returns a dyno instance of your type.|
| NewList      | object ||List\<object\>| Creates a dyno instance list of your object. Type is auto fetched from the object.|
| NewList      | Type ||List\<object\>| Creates a dyno instance list of your type.|

## DynoFilterAction enum API
The following enums are currently only needed to be used on DynoPropertyValues\<object\>

| Name | Value | Description |
| ------------- |:--------:||
|NO_ACTION| 0 |No modification action is performedon the property values upon calling DynoPropertyValues extension method|
|KEEP| 1 | Keeping the provided token on the pointed propertyName's value
|REMOVE| 2 |Removing the provided token on the pointed propertyName's value|

# Maintainers

I'm currently the only person to maintain the library.
