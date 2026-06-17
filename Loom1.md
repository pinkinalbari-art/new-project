# Antaran Digital Loom - Motif Editor Prototype

## Setup Instructions
This application requires absolutely zero installation or server setup. 
1. Download the `loom.html` file to your machine.
2. Double-click the file to open it instantly in any modern web browser (Chrome, Edge, Firefox, or Safari).

## Data Structure Explanation
The 16x16 grid canvas is managed via a single-dimensional flat array of 256 elements (`let gridState = Array(256).fill(null);`).
* Direct Index Mapping: Each array slot maps directly to a specific tile index on the CSS grid layout, keeping state tracking completely predictable.
* State Storage: Elements in the array store a color string value (e.g., '#e74c3c') when drawn on, or return to `null` when cleared or erased.
* Performance Efficiency: This flat data matrix allows for constant-time O(1) state lookups and updates, bypassing the nested loop overhead common with 2D coordinate matrices.

## Price Estimation Logic
The interactive price estimation engine recalculates reactively whenever grid data changes:
* Base Price: A fixed operational overhead of ₹500.
* Complexity Surcharge: Active knots are isolated by filtering out null slots from the array state. Every painted pixel unit adds a fee of ₹2.
* Thread Color Charge: A native JavaScript `Set` parses out duplicate values from the filled states array to determine total unique colors used. Each unique thread profile increments cost by ₹50.
* Pricing Formula: Total Price = 500 + (Filled Cells * 2) + (Unique Colors * 50)
