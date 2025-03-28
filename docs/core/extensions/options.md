---
title: Options pattern
author: IEvangelist
description: Learn the options pattern to represent groups of related settings in .NET apps. The options pattern uses classes to provide strongly-typed access to settings.
ms.author: dapine
ms.date: 08/13/2024
---

# Options pattern in .NET

The options pattern uses classes to provide strongly typed access to groups of related settings. When [configuration settings](configuration.md) are isolated by scenario into separate classes, the app adheres to two important software engineering principles:

- The [Interface Segregation Principle (ISP) or Encapsulation](../../architecture/modern-web-apps-azure/architectural-principles.md#encapsulation): Scenarios (classes) that depend on configuration settings depend only on the configuration settings that they use.
- [Separation of Concerns](../../architecture/modern-web-apps-azure/architectural-principles.md#separation-of-concerns): Settings for different parts of the app aren't dependent or coupled with one another.

Options also provide a mechanism to validate configuration data. For more information, see the [Options validation](#options-validation) section.

## Bind hierarchical configuration

The preferred way to read related configuration values is using the options pattern. The options pattern is possible through the <xref:Microsoft.Extensions.Options.IOptions%601> interface, where the generic type parameter `TOptions` is constrained to a `class`. The `IOptions<TOptions>` can later be provided through dependency injection. For more information, see [Dependency injection in .NET](dependency-injection.md).

For example, to read the highlighted configuration values from an _appsettings.json_ file:

:::code language="json" source="snippets/configuration/console-json/appsettings.json" highlight="3-6":::

Create the following `TransientFaultHandlingOptions` class:

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs" range="3-7":::

<span id="options-class"></span>
When using the options pattern, an options class:

- Must be non-abstract with a public parameterless constructor
- Contain public read-write properties to bind (fields are ***not*** bound)

The following code is part of the _Program.cs_ C# file and:

* Calls [ConfigurationBinder.Bind](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind%2A) to bind the `TransientFaultHandlingOptions` class to the `"TransientFaultHandlingOptions"` section.
* Displays the configuration data.

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" highlight="15-20" range="1-29":::

In the preceding code, the JSON configuration file has its `"TransientFaultHandlingOptions"` section bound to the `TransientFaultHandlingOptions` instance. This hydrates the C# objects properties with those corresponding values from the configuration.

[`ConfigurationBinder.Get<T>`](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get%2A) binds and returns the specified type. `ConfigurationBinder.Get<T>` may be more convenient than using `ConfigurationBinder.Bind`. The following code shows how to use `ConfigurationBinder.Get<T>` with the `TransientFaultHandlingOptions` class:

```csharp
var options =
    builder.Configuration.GetSection(nameof(TransientFaultHandlingOptions))
        .Get<TransientFaultHandlingOptions>();

Console.WriteLine($"TransientFaultHandlingOptions.Enabled={options.Enabled}");
Console.WriteLine($"TransientFaultHandlingOptions.AutoRetryDelay={options.AutoRetryDelay}");
```

In the preceding code, the `ConfigurationBinder.Get<T>` is used to acquire an instance of the `TransientFaultHandlingOptions` object with its property values populated from the underlying configuration.

> [!IMPORTANT]
> The <xref:Microsoft.Extensions.Configuration.ConfigurationBinder> class exposes several APIs, such as `.Bind(object instance)` and `.Get<T>()` that are ***not*** constrained to `class`. When using any of the [Options interfaces](#options-interfaces), you must adhere to aforementioned [options class constraints](#options-class).

An alternative approach when using the options pattern is to bind the `"TransientFaultHandlingOptions"` section and add it to the [dependency injection service container](dependency-injection.md). In the following code, `TransientFaultHandlingOptions` is added to the service container with <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure%2A> and bound to configuration:

```csharp
HostApplicationBuilder builder = Host.CreateApplicationBuilder(args);

builder.Services.Configure<TransientFaultHandlingOptions>(
    builder.Configuration.GetSection(
        key: nameof(TransientFaultHandlingOptions)));
```

The `builder` in the preceding example is an instance of <xref:Microsoft.Extensions.Hosting.HostApplicationBuilder>.

> [!TIP]
> The `key` parameter is the name of the configuration section to search for. It does *not* have to match the name of the type that represents it. For example, you could have a section named `"FaultHandling"` and it could be represented by the `TransientFaultHandlingOptions` class. In this instance, you'd pass `"FaultHandling"` to the <xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A> function instead. The `nameof` operator is used as a convenience when the named section matches the type it corresponds to.

Using the preceding code, the following code reads the position options:

:::code language="csharp" source="snippets/configuration/console-json/ExampleService.cs":::

In the preceding code, changes to the JSON configuration file after the app has started are ***not*** read. To read changes after the app has started, use [IOptionsSnapshot](#use-ioptionssnapshot-to-read-updated-data) or [IOptionsMonitor](#ioptionsmonitor) to monitor changes as they occur, and react accordingly.

## Options interfaces

<xref:Microsoft.Extensions.Options.IOptions%601>:

- Does ***not*** support:
  - Reading of configuration data after the app has started.
  - [Named options](#named-options-support-using-iconfigurenamedoptions)
- Is registered as a [Singleton](dependency-injection.md#singleton) and can be injected into any [service lifetime](dependency-injection.md#service-lifetimes).

<xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>:

- Is useful in scenarios where options should be recomputed on every injection resolution, in [scoped or transient lifetimes](dependency-injection.md#service-lifetimes). For more information, see [Use IOptionsSnapshot to read updated data](#use-ioptionssnapshot-to-read-updated-data).
- Is registered as [Scoped](dependency-injection.md#scoped) and therefore cannot be injected into a Singleton service.
- Supports [named options](#named-options-support-using-iconfigurenamedoptions).

<xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:

- Is used to retrieve options and manage options notifications for `TOptions` instances.
- Is registered as a [Singleton](dependency-injection.md#singleton) and can be injected into any [service lifetime](dependency-injection.md#service-lifetimes).
- Supports:
  - Change notifications
  - [Named options](#named-options-support-using-iconfigurenamedoptions)
  - [Reloadable configuration](#use-ioptionssnapshot-to-read-updated-data)
  - Selective options invalidation (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601>)

<xref:Microsoft.Extensions.Options.IOptionsFactory%601> is responsible for creating new options instances. It has a single <xref:Microsoft.Extensions.Options.IOptionsFactory%601.Create%2A> method. The default implementation takes all registered <xref:Microsoft.Extensions.Options.IConfigureOptions%601> and <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601> and runs all the configurations first, followed by the post-configuration. It distinguishes between <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> and <xref:Microsoft.Extensions.Options.IConfigureOptions%601> and only calls the appropriate interface.

<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> is used by <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> to cache `TOptions` instances. The <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> invalidates options instances in the monitor so that the value is recomputed (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryRemove%2A>). Values can be manually introduced with <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryAdd%2A>. The <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.Clear%2A> method is used when all named instances should be recreated on demand.

<xref:Microsoft.Extensions.Options.IOptionsChangeTokenSource%601> is used to fetch the <xref:Microsoft.Extensions.Primitives.IChangeToken> that tracks changes to the underlying `TOptions` instance. For more information on change-token primitives, see [Change notifications](primitives.md).

### Options interfaces benefits

Using a generic wrapper type gives you the ability to decouple the lifetime of the option from the dependency injection (DI) container. The <xref:Microsoft.Extensions.Options.IOptions%601.Value?displayProperty=nameWithType> interface provides a layer of abstraction, including generic constraints, on your options type. This provides the following benefits:

- The evaluation of the `T` configuration instance is deferred to the accessing of <xref:Microsoft.Extensions.Options.IOptions%601.Value?displayProperty=nameWithType>, rather than when it is injected. This is important because you can consume the `T` option from various places and choose the lifetime semantics without changing anything about `T`.
- When registering options of type `T`, you do not need to explicitly register the `T` type. This is a convenience when you're [authoring a library](options-library-authors.md) with simple defaults, and you don't want to force the caller to register options into the DI container with a specific lifetime.
- From the perspective of the API, it allows for constraints on the type `T` (in this case, `T` is constrained to a reference type).

## Use IOptionsSnapshot to read updated data

When you use <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>, options are computed once per request when accessed and are cached for the lifetime of the request. Changes to the configuration are read after the app starts when using configuration providers that support reading updated configuration values.

The difference between `IOptionsMonitor` and `IOptionsSnapshot` is that:

- `IOptionsMonitor` is a [singleton service](dependency-injection.md#singleton) that retrieves current option values at any time, which is especially useful in singleton dependencies.
- `IOptionsSnapshot` is a [scoped service](dependency-injection.md#scoped) and provides a snapshot of the options at the time the `IOptionsSnapshot<T>` object is constructed. Options snapshots are designed for use with transient and scoped dependencies.

The following code uses <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>.

:::code language="csharp" source="snippets/configuration/console-json/ScopedService.cs":::

The following code registers a configuration instance which `TransientFaultHandlingOptions` binds against:

```csharp
builder.Services
    .Configure<TransientFaultHandlingOptions>(
        configurationRoot.GetSection(
            nameof(TransientFaultHandlingOptions)));
```

In the preceding code, the `Configure<TOptions>` method is used to register a configuration instance that `TOptions` will bind against, and updates the options when the configuration changes.

## IOptionsMonitor

The `IOptionsMonitor` type supports change notifications and enables scenarios where your app may need to respond to configuration source changes dynamically. This is useful when you need to react to changes in configuration data after the app has started. Change notifications are only supported for file-system based configuration providers, such as the following:

- [Microsoft.Extensions.Configuration.Ini](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini)
- [Microsoft.Extensions.Configuration.Json](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json)
- [Microsoft.Extensions.Configuration.KeyPerFile](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.KeyPerFile)
- [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets)
- [Microsoft.Extensions.Configuration.Xml](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml)

To use the options monitor, options objects are configured in the same way from a configuration section.

```csharp
builder.Services
    .Configure<TransientFaultHandlingOptions>(
        configurationRoot.GetSection(
            nameof(TransientFaultHandlingOptions)));
```

The following example uses <xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:

:::code language="csharp" source="snippets/configuration/console-json/MonitorService.cs":::

In the preceding code, changes to the JSON configuration file after the app has started are read.

> [!TIP]
> Some file systems, such as Docker containers and network shares, may not reliably send change notifications. When using the <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> interface in these environments, set the `DOTNET_USE_POLLING_FILE_WATCHER` environment variable to `1` or `true` to poll the file system for changes. The interval at which changes are polled is every four seconds and is not configurable.
>
> For more information on Docker containers, see [Containerize a .NET app](../docker/build-container.md).

## Named options support using IConfigureNamedOptions

Named options:

- Are useful when multiple configuration sections bind to the same properties.
- Are case-sensitive.

Consider the following *appsettings.json* file:

```json
{
  "Features": {
    "Personalize": {
      "Enabled": true,
      "ApiKey": "aGEgaGEgeW91IHRob3VnaHQgdGhhdCB3YXMgcmVhbGx5IHNvbWV0aGluZw=="
    },
    "WeatherStation": {
      "Enabled": true,
      "ApiKey": "QXJlIHlvdSBhdHRlbXB0aW5nIHRvIGhhY2sgdXM/"
    }
  }
}
```

Rather than creating two classes to bind `Features:Personalize` and `Features:WeatherStation`,
the following class is used for each section:

```csharp
public class Features
{
    public const string Personalize = nameof(Personalize);
    public const string WeatherStation = nameof(WeatherStation);

    public bool Enabled { get; set; }
    public string ApiKey { get; set; }
}
```

The following code configures the named options:

```csharp
HostApplicationBuilder builder = Host.CreateApplicationBuilder(args);

// Omitted for brevity...

builder.Services.Configure<Features>(
    Features.Personalize,
    builder.Configuration.GetSection("Features:Personalize"));

builder.Services.Configure<Features>(
    Features.WeatherStation,
    builder.Configuration.GetSection("Features:WeatherStation"));
```

The following code displays the named options:

```csharp
public sealed class Service
{
    private readonly Features _personalizeFeature;
    private readonly Features _weatherStationFeature;

    public Service(IOptionsSnapshot<Features> namedOptionsAccessor)
    {
        _personalizeFeature = namedOptionsAccessor.Get(Features.Personalize);
        _weatherStationFeature = namedOptionsAccessor.Get(Features.WeatherStation);
    }
}
```

All options are named instances. <xref:Microsoft.Extensions.Options.IConfigureOptions%601> instances are treated as targeting the `Options.DefaultName` instance, which is `string.Empty`. <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> also implements <xref:Microsoft.Extensions.Options.IConfigureOptions%601>. The default implementation of the <xref:Microsoft.Extensions.Options.IOptionsFactory%601> has logic to use each appropriately. The `null` named option is used to target all of the named instances instead of a specific named instance. <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll%2A> and <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> use this convention.

## OptionsBuilder API

<xref:Microsoft.Extensions.Options.OptionsBuilder%601> is used to configure `TOptions` instances. `OptionsBuilder` streamlines creating named options as it's only a single parameter to the initial `AddOptions<TOptions>(string optionsName)` call instead of appearing in all of the subsequent calls. Options validation and the `ConfigureOptions` overloads that accept service dependencies are only available via `OptionsBuilder`.

`OptionsBuilder` is used in the [Options validation](#options-validation) section.

## Use DI services to configure options

When you're configuring options, you can use [dependency injection](dependency-injection.md) to access registered services, and use them to configure options. This is useful when you need to access services to configure options. Services can be accessed from DI while configuring options in two ways:

- Pass a configuration delegate to [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) on [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder%601). `OptionsBuilder<TOptions>` provides overloads of [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) that allow use of up to five services to configure options:

  ```csharp
  builder.Services
      .AddOptions<MyOptions>("optionalName")
      .Configure<ExampleService, ScopedService, MonitorService>(
          (options, es, ss, ms) =>
              options.Property = DoSomethingWith(es, ss, ms));
  ```

- Create a type that implements <xref:Microsoft.Extensions.Options.IConfigureOptions%601> or <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> and register the type as a service.

It's recommended to pass a configuration delegate to [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A), since creating a service is more complex. Creating a type is equivalent to what the framework does when calling [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A). Calling [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) registers a transient generic <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601>, which has a constructor that accepts the generic service types specified.

## Options validation

Options validation enables option values to be validated.

Consider the following *appsettings.json* file:

```json
{
  "MyCustomSettingsSection": {
    "SiteTitle": "Amazing docs from Awesome people!",
    "Scale": 10,
    "VerbosityLevel": 32
  }
}
```

The following class binds to the `"MyCustomSettingsSection"` configuration section and applies a couple of `DataAnnotations` rules:

:::code language="csharp" source="snippets/configuration/console-json/SettingsOptions.cs":::

In the preceding `SettingsOptions` class, the `ConfigurationSectionName` property contains the name of the configuration section to bind to. In this scenario, the options object provides the name of its configuration section.

> [!TIP]
> The configuration section name is independent of the configuration object that it's binding to. In other words, a configuration section named `"FooBarOptions"` can be bound to an options object named `ZedOptions`. Although it might be common to name them the same, it's *not* necessary and can actually cause name conflicts.

The following code:

- Calls <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%2A> to get an [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder%601) that binds to the `SettingsOptions` class.
- Calls <xref:Microsoft.Extensions.DependencyInjection.OptionsBuilderDataAnnotationsExtensions.ValidateDataAnnotations%2A> to enable validation using `DataAnnotations`.

```csharp
builder.Services
    .AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.ConfigurationSectionName))
    .ValidateDataAnnotations();
```

The `ValidateDataAnnotations` extension method is defined in the [Microsoft.Extensions.Options.DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) NuGet package.

The following code displays the configuration values or reports validation errors:

:::code language="csharp" source="snippets/configuration/console-json/ValidationService.cs":::

The following code applies a more complex validation rule using a delegate:

```csharp
builder.Services
    .AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.ConfigurationSectionName))
    .ValidateDataAnnotations()
    .Validate(config =>
    {
        if (config.Scale != 0)
        {
            return config.VerbosityLevel > config.Scale;
        }

        return true;
    }, "VerbosityLevel must be > than Scale.");
```

The validation occurs at run time, but you can configure it to occur at startup by instead chaining a call to `ValidateOnStart`:

```csharp
builder.Services
    .AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.ConfigurationSectionName))
    .ValidateDataAnnotations()
    .Validate(config =>
    {
        if (config.Scale != 0)
        {
            return config.VerbosityLevel > config.Scale;
        }

        return true;
    }, "VerbosityLevel must be > than Scale.")
    .ValidateOnStart();
```

Starting with .NET 8, you can use an alternate API, <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptionsWithValidateOnStart%60%601(Microsoft.Extensions.DependencyInjection.IServiceCollection,System.String)>, that enables validation on start for a specific options type:

```csharp
builder.Services
    .AddOptionsWithValidateOnStart<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.ConfigurationSectionName))
    .ValidateDataAnnotations()
    .Validate(config =>
    {
        if (config.Scale != 0)
        {
            return config.VerbosityLevel > config.Scale;
        }

        return true;
    }, "VerbosityLevel must be > than Scale.");
```

### `IValidateOptions` for complex validation

The following class implements <xref:Microsoft.Extensions.Options.IValidateOptions%601>:

:::code language="csharp" source="snippets/configuration/console-json/ValidateSettingsOptions.cs":::

`IValidateOptions` enables moving the validation code into a class.

> [!NOTE]
> This example code relies on the [Microsoft.Extensions.Configuration.Json](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) NuGet package.

Using the preceding code, validation is enabled when configuring services with the following code:

```csharp
HostApplicationBuilder builder = Host.CreateApplicationBuilder(args);

// Omitted for brevity...

builder.Services.Configure<SettingsOptions>(
    builder.Configuration.GetSection(
        SettingsOptions.ConfigurationSectionName));

builder.Services.TryAddEnumerable(
    ServiceDescriptor.Singleton
        <IValidateOptions<SettingsOptions>, ValidateSettingsOptions>());
```

## Options post-configuration

Set post-configuration with <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601>. Post-configuration runs after all <xref:Microsoft.Extensions.Options.IConfigureOptions%601> configuration occurs, and can be useful in scenarios when you need to override configuration:

```csharp
builder.Services.PostConfigure<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

<xref:Microsoft.Extensions.Options.IPostConfigureOptions%601.PostConfigure%2A> is available to post-configure named options:

```csharp
builder.Services.PostConfigure<CustomOptions>("named_options_1", customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

Use <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> to post-configure all configuration instances:

```csharp
builder.Services.PostConfigureAll<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

## See also

- [Configuration in .NET](configuration.md)
- [Options pattern guidance for .NET library authors](options-library-authors.md)
