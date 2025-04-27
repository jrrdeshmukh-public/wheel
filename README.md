# Auto Trader - Interactive Trading Dashboard

This project implements an **interactive options trading dashboard** using **C++**, **OpenGL**, **GLFW**, **ImGui**, and a **custom TWS client** (Interactive Brokers API).

It connects to a live TWS (Trader Workstation) or IB Gateway instance to allow:
- Viewing account summaries
- Managing available stock positions for covered call opportunities
- Filtering and selecting option contracts
- Building an order cart
- Placing options orders interactively

---

## Key Features

### ✨ Real-Time Trading Dashboard
- Live connection to TWS for account updates, positions, and options data.
- Display margin, available funds, day trades remaining.

### 📈 Covered Calls Automation
- Identify covered call opportunities automatically from owned stock positions.
- Manage call placement easily with quantity selection and quick routing.

### 🔎 Intelligent Options Filtering
- Query available options contracts.
- Filter based on **days to expiry** and **strike-to-price delta** range.
- Preview filtered options dynamically.

### 🛒 Cart System
- Add filtered options to a **Cart** before placing.
- Edit quantities and remove items.
- Batch-place multiple orders at once.

---

## How It Works

1. **Startup**: Initializes OpenGL, GLFW, and ImGui. Connects to TWS at `localhost:4000`.
2. **Main UI**: Single unified window with 3 tabs:
   - **Available Options**: Shows stock positions and possible covered calls.
   - **Options Selector**: Filters and displays available option contracts.
   - **Cart**: Holds orders ready to be placed.

3. **Routing and Placing Orders**:
   - User selects stock, filters contracts, adds options to cart.
   - Orders are placed by sending them through the TWS client interface.

---

## Dependencies

- **GLEW**: OpenGL extension wrangler library
- **GLFW**: OpenGL window and input management
- **ImGui**: Immediate Mode GUI for C++
- **Interactive Brokers C++ API**: 
  - `EClientSocket`, `EWrapper`, `Contract`, `Order`, etc.
  - Custom wrapper client (`CppClient`) provided.

---

## Code Structure

| File                     | Purpose                                            |
|---------------------------|----------------------------------------------------|
| `main.cpp`                | Main application logic and UI rendering            |
| `CppClient.h/.cpp`        | Client wrapper for IB API                          |
| `ContractSamples.h`       | Example contracts for different asset types        |
| `OrderSamples.h`          | Example orders (Market, Limit, etc.)               |
| `Utils.h`                 | Helper functions                                   |

---

## Main Components

### Client Interaction
- `CppClient` handles connection, stock price queries, account summaries, options chain queries, and order placement.

### UI Components
- **Account Summary**: Net liquidation, funds, day trade info.
- **Options Discovery**: Shows your current stock positions and available call writing opportunities.
- **Options Filtering**: Filter by delta and expiry range.
- **Cart Management**: View, modify, and send option orders.

### State Management
- `currentTab`: Controls the current active ImGui tab.
- `routedSymbol`, `routedContracts`: Manage selected symbol and contracts routing.
- Caching:
  - Stock prices
  - Account list
  - Option trades
  - Option contracts

---

## Building and Running

### Prerequisites

- C++17+ compiler
- GLEW, GLFW, and ImGui installed
- Interactive Brokers TWS or IB Gateway running
- IB API C++ headers and libraries

### Build (Example with g++)

```bash
g++ main.cpp CppClient.cpp -o AutoTrader \
