# Wheel - Interactive Options Trading Dashboard

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
- Add filtered options to a cart.
- Manage quantities and status.
- One-click placement of multiple options orders from the cart.

---

## Code Structure

### `main()`
- Initializes **GLFW**, **GLEW**, and **ImGui**.
- Creates a window and sets up rendering.
- Connects the `CppClient` to TWS on `localhost:4000`.
- Enters the render loop where `RenderUnifiedWindow()` is called each frame.

### `RenderUnifiedWindow(CppClient* client)`
- Builds the complete UI:
  - **Account Summary**: Pick an account and view details.
  - **Available Options**: View owned stocks and choose stocks for covered call writing.
  - **Options Selector**: Filter and select appropriate options contracts.
  - **Cart**: Manage and place orders.

### Data Fetching and Caching
- `getOrUseCachedAccountList()` - Fetch account list once.
- `getOrUseCachedAccountSummary()` - Fetch and cache account balances.
- `getOrUseCachedOptionsTrades()` - Fetch open stock positions and possible calls.
- `getOrUseCachedOptionContracts()` - Fetch available option contracts for a stock.
- `getOrUseCachedStockPrice()` - Fetch current stock prices when needed.

---

## Requirements

- **C++17** or later
- **GLEW** for OpenGL extensions
- **GLFW** for window creation and input
- **Dear ImGui** for UI rendering
- **Interactive Brokers C++ API** (EClientSocket, Contract, Order, etc.)

---

## Running the Application

1. Install and run TWS or IB Gateway locally.
2. Enable API Access in TWS:
   - Configure > API > Settings > Enable ActiveX and Socket Clients
   - Set socket port to `4000`
3. Build the project with a C++ compiler.
4. Run the executable:
   ```bash
   ./wheel
