# CafeApp ☕

A Windows desktop application built with C# and Windows Forms that simulates a cafe ordering system. Users can browse a menu of coffee drinks, select quantities, build a basket, and view an itemized order summary with a running total. Prices are displayed in South African Rand (ZAR).

## Table of Contents

- [Features](#features)
- [Menu](#menu)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Building for Release](#building-for-release)

## Features

- **Drink Selection** - Choose from a curated menu of popular coffee drinks via a dropdown
- **Quantity Control** - Set how many of each drink you want using a numeric spinner (defaults to 1)
- **Add to Basket** - Build up your order one item at a time
- **Order Summary** - View all items in your basket with individual line prices and a calculated grand total
- **Clean UI** - Simple, intuitive two-panel layout with controls on the left and the order summary on the right

## Menu

| Drink      | Price (ZAR) |
| ---------- | ----------- |
| Americano  | R15         |
| Espresso   | R20         |
| Cappuccino | R25         |
| Latte      | R30         |

## Screenshots

> _Screenshots coming soon. Run the application to see the UI in action._

## Tech Stack

| Component | Technology               |
| --------- | ------------------------ |
| Language  | C# 12                    |
| Framework | .NET 8 (Windows Desktop) |
| UI        | Windows Forms (WinForms) |
| IDE       | Visual Studio 2022       |

## Prerequisites

Before running CafeApp, make sure you have the following installed:

- **Windows 10 or later**
- **[.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)** (8.0 or newer)
- **Visual Studio 2022** (optional, but recommended for the full designer experience)
  - When installing via Visual Studio, ensure the **.NET desktop development** workload is selected

You can verify your .NET SDK installation by running:

```bash
dotnet --version
```

## Getting Started

### Option 1: Using the .NET CLI

1. **Clone the repository**

   ```bash
   git clone https://github.com/your-username/CafeApp.git
   cd CafeApp
   ```

2. **Restore dependencies**

   ```bash
   dotnet restore CafeApp/CafeApp.csproj
   ```

3. **Build the project**

   ```bash
   dotnet build CafeApp/CafeApp.csproj
   ```

4. **Run the application**

   ```bash
   dotnet run --project CafeApp/CafeApp.csproj
   ```

### Option 2: Using Visual Studio

1. Open `CafeApp/CafeApp.sln` in Visual Studio 2022
2. Set the build configuration to **Debug** or **Release**
3. Press **F5** (or click the green Start button) to build and run

## Project Structure

```text
CafeApp/
├── CafeApp.sln              # Visual Studio solution file
├── CafeApp.csproj            # Project file (.NET 8, WinForms)
├── Program.cs                # Application entry point
├── Form1.cs                  # Main form logic (event handlers, basket interaction)
├── Form1.Designer.cs         # Auto-generated UI layout and control definitions
├── Form1.resx                # Form resource file
├── Item.cs                   # Item model (drink name, quantity, price lookup)
├── Basket.cs                 # Basket model (item collection, display formatting, total calculation)
└── obj/                      # Build artifacts (auto-generated)
```

### Key Files

| File                | Description                                                                 |
| ------------------- | --------------------------------------------------------------------------- |
| `Program.cs`        | Entry point that initializes the application and launches the main form     |
| `Form1.cs`          | Handles user interactions: adding items to the basket and displaying orders |
| `Form1.Designer.cs` | Defines the form layout, controls, fonts, and sizing                        |
| `Item.cs`           | Represents a single menu item with name, quantity, and price                |
| `Basket.cs`         | Manages a collection of items and generates the formatted order summary     |

## How It Works

### Application Flow

1. The user selects a drink from the **ComboBox** dropdown (Espresso, Cappuccino, Latte, or Americano)
2. The user sets the desired quantity using the **NumericUpDown** spinner
3. Clicking **Add Item** creates a new `Item` instance and adds it to the `Basket`
4. Clicking **Display** renders the full basket contents in the **RichTextBox**, showing each item's name, quantity, and line price, followed by the total

### Architecture

The application follows a straightforward object-oriented design:

- **`Item`** - A model class that encapsulates a drink's name, quantity, and unit price. The price is determined automatically by a `switch` statement based on the drink name.
- **`Basket`** - A collection class that holds a `List<Item>` and provides methods to add items and generate a formatted display string. The total is calculated using LINQ's `Sum` method.
- **`Form1`** - The main form that ties the UI controls to the domain logic, acting as the controller between user input and the underlying models.

### Pricing Logic

When an `Item` is created, its unit price is assigned based on the drink name:

```csharp
switch (name)
{
    case "Espresso":    price = 20; break;
    case "Cappuccino":  price = 25; break;
    case "Latte":       price = 30; break;
    case "Americano":   price = 15; break;
}
```

The total is then calculated as the sum of `price * quantity` for every item in the basket.

## Building for Release

To create a release build for distribution:

```bash
dotnet publish CafeApp/CafeApp.csproj -c Release
```

The compiled output will be located in `CafeApp/bin/Release/net8.0-windows/publish/`.

For a **self-contained** build (includes the .NET runtime so users don't need it installed):

```bash
dotnet publish CafeApp/CafeApp.csproj -c Release --self-contained -r win-x64
```
