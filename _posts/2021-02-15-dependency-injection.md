---
layout: post
title: "Dependency Injection"
categories: Programming
excerpt: An introduction to Dependency Injection
---

I've recently released a post about Inversion of Control and dependency injection in a previous post [here](/inversion-of-control). Now I wanted to provide an example of how the design patten is used and why it's useful.

## Introduction &#x1f91d;

Imagine I have an application which stores entries to a blog. To get the data for the entries, I use an `EntryRepository` which will be responsible for querying the data, the application is a simple CRUD API but for now I'll only focus on reading the data:
```c#
public class EntryRepository
{
    public async Task<List<Entry>> ListEntries()
    {
        // Some logic here
    }
}
```

Within the EntryRepository, imagine that, at the moment, it needs to get the data from a class called `FileDataStore`, which extracts data from a CSV file

One way I can approach this is to instantiate the class like this:

```c#
public async Task<List<Entry>> ListEntries()
{
    var path = "/path/to/file.csv"
    var file = Path.Join(Path.GetDirectoryName(
        typeof(Program).Assembly.Location),
        path
    );
    var fileDataStore = new FileDataStore(file);
    return fileDataStore.GetAllEntries();
}
```

This would work, but the problem is that it causes **tight coupling** between those classes. And the reason why it matters is, not only is it difficult to test, it is also difficult to mainain.

For example, imagine that the entry repository also needs to be able to get entries from other data stores, perhaps from a class called `MySQLDataStore`. How would we achieve this? One option is to pass in a parameter to determine which data store to use:

```c#
public async Task<List<Entry>> ListEntries(bool useMySQL)
{
    if (useMySQL)
    {
        var dataStore = new MySQLDataStore();
        return dataStore.GetAllEntries();
    }
    else
    {
        var path = "/path/to/file.csv";
        var file = Path.Join(Path.GetDirectoryName(typeof(Program).Assembly.Location), path);
        var fileDataStore = new FileDataStore(file);
        return fileDataStore.GetAllEntries();
    }
}
```

At first glance that's not "too" bad, but what happens if there is also a third or even fourth data store added at a later date.

```c#
public async Task<List<Entry>> ListEntries(DataStoreEnum result)
{
    switch (result)
    {
        case DataStoreEnum.MySQL:
            var dataStore = new MySQLDataStore();
            return dataStore.GetAllEntries();
        case DataStoreEnum.CSV:
            var path = "/path/to/csv-file.csv";
            var file = Path.Join(Path.GetDirectoryName(typeof(Program).Assembly.Location), path);
            var fileDataStore = new FileDataStore(file);
            return fileDataStore.GetAllEntries();
        case DataStoreEnum.SqlServer:
            var dataStore = new SqlServerDataStore();
            return dataStore.GetAllEntries();
        case DataStoreEnum.Excel:
            var path = "/path/to/excel-file.xls";
            var file = Path.Join(Path.GetDirectoryName(typeof(Program).Assembly.Location), path);
            var fileDataStore = new ExcelDataStore(file);
            return fileDataStore.GetAllEntries();
        case DataStoreEnum.Json:
            var path = "/path/to/json-file.json";
            var file = Path.Join(Path.GetDirectoryName(typeof(Program).Assembly.Location), path);
            var fileDataStore = new JsonDataStore(file);
            return fileDataStore.GetAllEntries();
        default:
            return List<Entries>();
    }
}
```

As you can see, it's starting to grow and become harder to maintain. The logic deciding which data store to use also had to be updated.Even worse, what happens if we need to reuse this same group of potential datastores in other areas of the project.

Also, it's not impossible for even more data stores to be added or even different csv files which the FileDataStore can use but would need the path to the file.

As features or additional complexity are added, the code itself may need to drastically change in order to meet those requirements, even as far as potentially needing new parameters. Bearing in mind that everywhere this EntryRepository is being used will also need to be updated or monitored in case of errors and bugs.

While this example is a little silly and somewhat uncommon in many projects, we can imagine that, in a production environment, if we're not careful, the code of said project can become a nightmare to maintain.

And so the issue of tight coupling is not trivial, even for small projects, if it's a project with a long development cycle.

## Dependency Injection &#x1f489;

One solution to this problem is to apply the inversion of control principle and to remove the responsibility of creating the dependencies out of the EntryRepository. We can do this by combining the Dependency Inversion principle with the Dependency Injection design pattern.

To apply dependency injection pattern, we **inject** the dependency directly into the EntryRepository via it's constructor. What we also need to do is consider the dependency inversion principle which states that:

> High-level modules should not depend on low-level modules. Both should depend on the abstraction.

```c#
public interface IEntryRepository
{
    Task<List<Entry>> ListAsync();
}

public class EntryRepository : IEntryRepository
{
    private readonly IDataStore _dataStore;

    public EntryRepository(IDataStore dataStore)
    {
        _dataStore = dataStore;
    }

    public async Task<List<Entry>> ListAsync()
    {
        return await _dataStore.GetAllEntries().ToListAsync();
    }
}
```

By injecting the dependency into its constructor and having that being represented as an abstraction/interface in the code, this allows the "dependency" itself, be any form it wants to, so long as it implements that interface (`IDataStore`):

```c#
public interface IDataStore
{
    Task<List<Entry>> GetAllEntries();
}

public class MySQLDataStore : IDataStore
{
    public async Task<List<Entry>> GetAllEntries()
    {
        // code here
    }
}

public class SqlServerDataStore : IDataStore
{
    public async Task<List<Entry>> GetAllEntries()
    {
        // code here
    }
}

public class FileDataStore : IDataStore
{
    private readonly string _path;
    public EntryRepository(string path)
    {
        _path = path;
    }

    public async Task<List<Entry>> GetAllEntries()
    {
        // code here
    }
}
```

By doing this, whenever we're using the EntryRepository, it is up to the calling code to provide the dependency.

```c#
public void SomeMethod()
{
    var path = "/path/to/json-file.json";
    var file = Path.Join(Path.GetDirectoryName(typeof(Program).Assembly.Location), path);
    var fileDataStore = new JsonDataStore(file);
    var repository = new EntryRepository(fileDataStore)

    // some more logic here..
}
```

Not only is this easier to test, this is a lot easier to maintain. Imagine that the project wanted to no longer read from files and new development made to read from a new data store class.

So long as the new data store class implements the IDataStore interface, you would easily be able to swap and replace the dependency with the new one without rewriting the EntryRepository code at all including it's automated tests if any.

## Summary &#x1f4dd;

Dependency Injection is a very useful pattern to write clean code. While it is not always necessary it will make the maintainability and testibility of your applications easier and less brittle.

One issue this can create is the caller code having the burden of instantiating many dependencies which could include dependencies which have their own dependencies. This leads to the next piece of the puzzle which I'll write about soon, using an IoC Container framework to automatically deal with that problem.