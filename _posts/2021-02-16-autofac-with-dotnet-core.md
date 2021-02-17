---
layout: post
title: "Autofac with .Net Core"
categories: Programming
excerpt: IoC Container example with Autofac
---

<img src="/assets/media/autofac-1.png" style="height:200px; margin: auto">

I've recently added a post about Inversion of Control and IoC Containers in a previous post [here](/inversion-of-control), I also added another which covers dependency injection. Now I wanted to provide an example of an IoC Container used which will solve some of the issues that can arise when using dependency injection for more complex classes with many dependencies. And so I would like to write about this particular IoC Container: [Autofac](https://autofac.org/)

## What is Autofac?

Autofac is an Inversion of Control Container for .Net Core, ASP.NET Core, .Net Framework, Universal Windows apps and more. With this framework you can build containers with lambdas, types or pre-built instances of components and can also scan dependencies for registration.

## Example

So in my [last post](/dependency-injection) I demonstrated an example of dependency injection in action.

```c#
public void SomeMethod()
{
    var path = "/path/to/json-file.json";
    var file = Path.Join(Path.GetDirectoryName(typeof(Program).Assembly.Location), path);
    var fileDataStore = new JsonDataStore(file);
    var repository = new EntryRepository(fileDataStore);
    var entries = repository.GetEntries();

    // some more logic here..
}
```

Looks good so far but what if the complexity increases where dependencies of a class may have their own dependencies and those dependencies could even have their own.

```c#
public void SomeMethod()
{
    var path = "/path/to/json-file.json";
    var file = Path.Join(Path.GetDirectoryName(typeof(Program).Assembly.Location), path);
    var logger = new Logger(
        new LoggerDependency(new LoggerDependencyDependency()),
        new SecondLoggerDependency()
    );
    var fileDataStore = new JsonDataStore(file, logger);
    var repository = new EntryRepository(fileDataStore, logger);
    var entries = repository.GetEntries();

    // some more logic here..
}
```
As silly as this looks, it's a very possible problem and we're having to rely on the caller code to instantiate the classes which again leads to tight coupling.
And so to solve this problem we can use an IoC Container.

### IoC Container
IoC Container, also known as DI Container, is a framework for implementing **automatic** dependency injection. It managed object creation and it's life-time, and also injects dependencies to the class.

And so we can use this to automatically instantiating and inject the dependencies whenever it is needed.

```c#
// startup.cs
public class Startup
{
    // ....

    public void ConfigureContainer(ContainerBuilder builder)
    {
        builder.RegisterModule(new AutofacModule());
    }

    // ...
}

public class AutofacModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        base.Load(builder);
        builder.RegisterType<EntryRepository>().As<IEntryRepository>();
        builder.RegisterType<Logger>().As<ILogger>();
        builder.RegisterType<LoggerDependency>().As<ILoggerDependency>();
        builder.RegisterType<LoggerDependencyDependency>().As<ILoggerDependencyDependency>();
        builder.RegisterType<JsonDataStore>().As<IDataStore>();
    }
}
```

At it's core all we're needing to do is register the concrete classes and also which abstraction/interface it implements, autofac will automatically resolve the object creation if it sees the abstraction/interface being injected into a class via the constructor including the objects own dependencies. Autofac will then automatically dispose the objects it has resolved once they're no longer needed.


```c#

public class SomeClass
{
    private readonly IEntryRepository _entryRepository;

    public SomeClass(IEntryRepository entryRepository)
    {
        _entryRepository = entryRepository;
    }

    public void SomeMethod()
    {
        var entries = _entryRepository.GetEntries();

        // some more logic here..
    }
}
```

### What other benefits does this provide?

While using dependency injection with Autofac makes it easier to test and keep code maintainable. One other benefit is the ability to seemlessly swap out concreate dependencies so long as it implements the abstraction/interface. For example, if I wanted to use a different DataStore or Logger, I can design the new one making sure I implement the same interface and only replace that concrete type in the Autofac module, and so the new concreation will be applied without having to update any logic or code in other areas of the application.

```c#
public class AutofacModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        base.Load(builder);
        builder.RegisterType<SomeNewEntryRepository>().As<IEntryRepository>();
        builder.RegisterType<SomeNewLogger>().As<ILogger>();
        builder.RegisterType<SomeNewLoggerDependency>().As<ILoggerDependency>();
        builder.RegisterType<SomeNewLoggerDependencyDependency>().As<ILoggerDependencyDependency>();
        builder.RegisterType<SomeNewDataStore>().As<IDataStore>();
    }
}
```

## Dynamically Register Modules

As your project grows, having to maintain the autofac module can get a little tedious. One feature autofac provides is the ability to register by assembly

```c#
public class AutofacModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        base.Load(builder);
        builder.RegisterAssemblyTypes(Assembly.GetExecutingAssembly())
            .AsImplementedInterfaces()
            .InstancePerLifetimeScope();
    }
}
```

By doing this we can also remove the need to independently register our modules and to do it dynamically thus allowing developers to focus on building the application and being able injecting new dependencies without having to maintain the configuration.

## Summary &#x1f4dd;

A fairly simple and brief example of how autofac works. There are many other features Autofac provides that I haven't covered, and I hope to learn more about them as I dive deeper in the framework.


### External sources &#x1f4a1;

[Autofac](https://autofac.org/)

[Inversion of Control](/inversion-of-control)

[Dependency Injection](/dependency-injection)