# Noctura - Solstice

Noctura is a C# WinForms application that provides a runtime environment and development workspace for **NetDust**.

Built on the **C++ based ndr engine**, Noctura supports the NetDust runtime and provides a lightweight environment for writing and running NetDust code.

## Features

### NetDust Runtime

Noctura is built around the ndr engine, a C++ based runtime engine for NetDust.

It provides the foundation for executing NetDust applications within Noctura.

### Noctura Workspace

**Noctura Workspace** is a lightweight development environment for writing and working with NetDust code.

It is designed for simple and convenient NetDust development without requiring a full project setup.

### Noctura Extension

**Noctura Extension** allows developers to extend Noctura using **NLua**.

Extensions can be written in Lua and loaded into Noctura to add custom functionality and integrate additional features into the application.

### Architecture

- **Presentation / UI Layer** (C# / WinForms)
  - Noctura
  - Noctura Workspace / Extension
- **Runtime Layer**
  - NetDust Runtime
- **Core Engine** (C++)
  - NDR Engine
