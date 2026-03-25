+++
title = "Building a Simple Config Loader in Go"
date = 2026-03-25
description = "A practical Go example covering file reading, interfaces, and error handling."
[taxonomies]
tags = ["go", "backend", "json", "learning"]
+++

## Building a Simple Config Loader in Go

When building real-world applications, configuration management is one of the first practical problems you run into. Whether it's ports, feature flags, or environment-specific settings, having a clean way to read and work with configuration is essential.

In this post, we'll walk through a simple yet practical Go program that demonstrates three important concepts:

- Reading files
- Using interfaces
- Handling errors effectively

---

## 📦 The Goal

We want to:

1. Read a JSON configuration file
2. Parse it into a Go struct
3. Use an interface to interact with the configuration
4. Handle errors in a clean and idiomatic way

---

## 🧱 Defining the Configuration Structure

We start by defining a struct that mirrors our JSON:

```go
type Config struct {
    AppName      string
    Port         int
    Debug        bool
    Tags         []string
    IsDeprecated bool
}
```

This struct acts as the blueprint for our configuration file.

---

## 🔌 Introducing Interfaces

Instead of tightly coupling our code to the struct, we define an interface:

```go
type AppCfg interface {
    Summary()    string
    Deprecated() bool
}
```

Now we implement this interface on our `Config` struct:

```go
func (c Config) Summary() string {
    return fmt.Sprintf(`
    App's Name  : %s
    Port        : %d
    Debug Mode  : %t
    Tags        : %v
    Deprecated  : %t
    `, c.AppName, c.Port, c.Debug, c.Tags, c.IsDeprecated)
}

func (c Config) Deprecated() bool {
    return c.IsDeprecated
}
```

Go interfaces are implemented implicitly, which keeps things simple and flexible.

---

## 🖨️ Using the Interface

We define a function that works with the interface rather than the struct:

```go
func printAppCfg(apcfg AppCfg) {
    fmt.Println(apcfg.Summary())
    if apcfg.Deprecated() {
        fmt.Println("App has been deprecated!!")
    }
}
```

This makes the function reusable and easier to test.

---

## 📂 Reading the Configuration File

Now comes file reading and JSON parsing:

```go
func readConfigFile(path string) (Config, error) {
    data, err := os.ReadFile(path)
    if err != nil {
        return Config{}, fmt.Errorf("readConfigFile -- Failed to read file -- %w", err)
    }

    cfg := Config{}

    if err := json.Unmarshal(data, &cfg); err != nil {
        return Config{}, fmt.Errorf("readConfigFile -- Invalid JSON -- %w", err)
    }

    return cfg, nil
}
```

Key takeaways:

- `os.ReadFile` simplifies file handling
- `json.Unmarshal` maps JSON into structs
- Errors are wrapped using `%w` for better debugging

---

## 🚨 Error Handling Done Right

In `main`, we fail fast if something goes wrong:

```go
func main() {
    cfg, err := readConfigFile("conf.json")
    if err != nil {
        fmt.Println("main --", err)
        os.Exit(1)
    }

    printAppCfg(cfg)
}
```

This approach ensures that errors are visible and don't silently break the application.

---

## 📄 Example JSON

Here's a sample `conf.json`:

```json
{
  "AppName": "MyApp",
  "Port": 8080,
  "Debug": true,
  "Tags": ["go", "backend", "demo"],
  "IsDeprecated": false
}
```

---

## 🧠 Final Thoughts

This small example brings together some core Go concepts:

- Structs for modeling data
- Interfaces for abstraction
- File I/O and JSON parsing
- Idiomatic error handling

Even though it's simple, these patterns scale really well in larger systems.

---

## 🚀 Next Steps

You can extend this by:

- Adding environment variable overrides
- Supporting YAML/TOML configs
- Validating config values
- Watching files for live reload

Simple, practical, and very Go.