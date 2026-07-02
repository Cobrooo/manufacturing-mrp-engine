# MRP Engine — Frontend Dashboard

React-based dashboard for the Enterprise Material Requirements Planning 
(MRP) Engine. Visualizes Bill of Materials hierarchies, displays material 
shortage calculations, and enables procurement managers to approve or 
reject auto-generated Purchase Orders.

## Tech Stack

| Technology | Purpose |
|---|---|
| React.js | Frontend framework |
| Axios | HTTP client for backend API calls |
| react-d3-tree | BOM hierarchy tree visualization |

## Prerequisites

- Node.js 16+ installed
- Backend API running at `http://localhost:8080`
  (see [manufacturing-mrp-engine](https://github.com/Cobrooo/manufacturing-mrp-engine))

## Setup

```bash
npm install
npm start
```

Runs on `http://localhost:3000`

## Features

### Production Order Input
- Select a finished good from the dropdown
- Enter a target production quantity
- Click "Explode BOM" to trigger the calculation

### BOM Tree View
- Visual tree diagram of the product hierarchy
- Blue node = Finished Good (root)
- Red nodes = Raw materials with shortages
- Green nodes = Raw materials with sufficient stock

### Requirements Table
- Shows all raw materials with:
  - Gross Requirement (total needed from BOM)
  - On-Hand Stock (current warehouse stock)
  - Net Requirement (what actually needs to be ordered)
- Color-coded rows for instant shortage identification

### Purchase Order Dashboard
- Lists all pending Purchase Orders
- Approve or Reject each PO with one click
- Instant status notification after each action
- Refresh button to reload pending orders

## Project Structure

src/
api/
mrpApi.js              — Centralized Axios API client
components/
ProductSelector.jsx    — Product and quantity input form
BomTreeView.jsx        — react-d3-tree BOM visualization
MrpResultsTable.jsx    — Material requirements table
PurchaseOrderPanel.jsx — PO approval dashboard
SummaryStats.jsx       — Summary cards (totals, shortages)
Spinner.jsx            — Loading indicator
ErrorMessage.jsx       — Error display with retry
App.js                   — Main layout and state management


## Backend API Endpoints Used

| Method | Endpoint | Used For |
|---|---|---|
| GET | `/api/items/finished-goods` | Populate product dropdown |
| GET | `/api/items/{id}` | Get selected product name |
| POST | `/api/mrp/explode` | Run BOM explosion |
| GET | `/api/inventory` | Fetch stock levels |
| GET | `/api/purchase-orders/status/PENDING` | Load pending POs |
| PUT | `/api/purchase-orders/{id}/approve` | Approve a PO |
| PUT | `/api/purchase-orders/{id}/reject` | Reject a PO |