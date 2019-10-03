# FSharp.Interop.Dynamic [![NuGet Status](http://img.shields.io/nuget/v/FSharp.Interop.Dynamic.svg?style=flat)](https://www.nuget.org/packages/FSharp.Interop.Dynamic/)


The F# Dynamic Operator, powered by the DLR. Compiled for .NET Standard 2.0, .NET Standard 1.6, .NET Framework 4.5

Install from [NuGet](https://nuget.org/packages/FSharp.Interop.Dynamic/)
```
PM> Install-Package FSharp.Interop.Dynamic
```

# Build Status

Platform | Status
-------- | ------
Nuget Deployment | [![Build status](https://ci.appveyor.com/api/projects/status/tbw9put64a0p3j9o/branch/master?svg=true)](https://ci.appveyor.com/project/jbtule/fsharp-dynamic-832/branch/master)
Mac/Linux/Windows | [![Action Status](https://github.com/fsprojects/FSharp.Interop.Dynamic/workflows/.NET%20Core%20CI/badge.svg)](https://github.com/fsprojects/FSharp.Interop.Dynamic/actions?workflow=.NET+Core+CI)
Coverage| [![codecov](https://codecov.io/gh/fsprojects/FSharp.Interop.Dynamic/branch/master/graph/badge.svg)](https://codecov.io/gh/fsprojects/FSharp.Interop.Dynamic) [![Coverage Status](https://coveralls.io/repos/github/fsprojects/FSharp.Interop.Dynamic/badge.svg?branch=master)](https://coveralls.io/github/fsprojects/FSharp.Interop.Dynamic?branch=master)
 
 
# Bleeding edge feed on MyGet

[![MyGet Pre Release](https://img.shields.io/myget/dynamitey-ci/vpre/FSharp.Interop.Dynamic.svg)](https://www.myget.org/feed/dynamitey-ci/package/nuget/FSharp.Interop.Dynamic)

# Usage

`target?Property`, `target?Property<-value`, and `target?Method(arg,arg2)` allow you to dynamically get/set properties and call methods

Also `Dyn.implicitConvert`,`Dyn.explicitConvert`, comparison operators and more.


# Examples:

### System.Dynamic
```fsharp
open FSharp.Interop.Dynamic
let ex1 = ExpandoObject()
ex1?Test<-"Hi"//Set Dynamic Property
ex1?Test //Get Dynamic
```

### SignalR

```fsharp
open FSharp.Interop.Dynamic
type MyHub =
    inherit Hub
    member x.Send (name : string) (message : string) =
        base.Clients.All?addMessage(name,message) |> ignore
```
### MVC ViewBag

```fsharp
x.ViewBag?Name<-"George"
```

# Caveats:

The `DLR` is incompatible with interface explicit members, so are these operators, [just like C#'s `dynamic` keyword](http://stackoverflow.com/questions/22514892/iterate-through-a-dictionary-inserted-in-a-asp-net-mvc4-pages-viewdata-via-f-c).

[.NET Core 2.0.0 to 2.0.2 had a major bug in the C# dynamic keyword with nested classes inside of generic classes.](https://github.com/fsprojects/FSharp.Interop.Dynamic/issues/11). You will know it from a substring argument length exception. .NET Framework 4.0+, .NET Core 1.x and .NET Core 2.0.3+ are unaffected.

## Maintainer(s)

- [@jbtule](https://github.com/jbtule)
- [@forki](https://github.com/forki)

The default maintainer account for projects under "fsprojects" is [@fsprojectsgit](https://github.com/fsprojectsgit) - F# Community Project Incubation Space (repo management)
