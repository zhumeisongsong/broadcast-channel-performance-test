# 🚀 BroadcastChannel Multi-Tab Performance Test

> A comprehensive performance testing suite for the browser BroadcastChannel API, designed to evaluate message transmission performance across different scenarios and configurations.

## 📋 Project Overview

BroadcastChannel API is a Web standard that enables communication between different tabs, iframes, or workers within the same origin. This project provides multiple test scenarios to assess its real-world performance characteristics, including latency, throughput, and scalability metrics.

## 🧪 Test Components

| Component                   | Purpose                | Key Features                                                    |
| --------------------------- | ---------------------- | --------------------------------------------------------------- |
| **`index.html`**            | Basic Performance Test | Multi-tab broadcast, latency measurement, real-time display     |
| **`publisher.html`**        | Message Publisher      | Configurable size/speed, start/stop control, publishing history |
| **`customer-sync.html`**    | Consumer with Sync     | Cross-tab sync, real-time metrics, request-response mode        |
| **`customer-no-sync.html`** | Independent Consumer   | Standalone processing, local stats, sync overhead comparison    |

## Performance Test Cases

**Consumer Request** is a pull-based messaging pattern where consumers actively request messages from the publisher instead of passively receiving them.

## ⚠️ Background Tab Throttling

When the publisher tab is in the background, browser throttling will significantly impact performance.

In the test case `Continuous medium message test`,

### **Key Effects**:

- **Timer Throttling**: `setInterval`/`setTimeout` minimum becomes ≈1000ms (Chrome/Edge/Firefox desktop), `requestAnimationFrame` stops
- **CPU/Time Inaccuracy**: Timers queue up and batch trigger, causing uneven message timestamps and significantly reduced throughput
- **Possible Freezing**: In certain scenarios (mobile, power saving, long-term background), tabs may enter freeze/suspend state, completely stopping JS execution
- **Message Delivery**: BroadcastChannel remains functional, but message generation is affected by throttling/freezing, resulting in fewer or clustered messages

### **Recommendations**:

- Keep publisher tab in foreground during performance testing
- Use request-response mode for background operation scenarios
- Monitor tab visibility state to avoid misinterpreting performance data

| Message Size (KB) | Publish Speed (ms) | Consumer Request (1s) | customer-sync.html                                                                                              | customer-no-sync.html | Test Strategy                      |
| ----------------- | ------------------ | --------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------- | ---------------------------------- |
| 10KB              | 50ms               | ✅                    | --                                                                                                              | --                    | --                                 |
| 10KB              | 50ms               | ❌                    | --                                                                                                              | --                    | --                                 |
| 10KB              | 100ms              | ✅                    | --                                                                                                              | --                    | --                                 |
| 10KB              | 100ms              | ❌                    | --                                                                                                              | --                    | --                                 |
| 10KB              | 500ms              | ✅                    | --                                                                                                              | --                    | --                                 |
| 10KB              | 500ms              | ❌                    | --                                                                                                              | --                    | --                                 |
| 100KB             | 50ms               | ✅                    | The messages per second count drops from 20 to 2–3 when the publisher tab is in the background.                 | Same as sync          | High frequency medium message test |
| 100KB             | 50ms               | ❌                    | The messages per second count is stable.                                                                        | Same as sync          | Continuous medium message test     |
| 100KB             | 100ms              | ✅                    | --                                                                                                              | --                    | Balanced medium message test       |
| 100KB             | 100ms              | ❌                    | --                                                                                                              | --                    | Standard medium message test       |
| 100KB             | 500ms              | ✅                    | --                                                                                                              | --                    | --                                 |
| 100KB             | 500ms              | ❌                    | --                                                                                                              | --                    | --                                 |
| 500KB             | 50ms               | ✅                    | --                                                                                                              | --                    | --                                 |
| 500KB             | 50ms               | ❌                    | --                                                                                                              | --                    | --                                 |
| 500KB             | 100ms              | ✅                    | --                                                                                                              | --                    | --                                 |
| 500KB             | 100ms              | ❌                    | --                                                                                                              | --                    | --                                 |
| 500KB             | 500ms              | ✅                    | --                                                                                                              | --                    | --                                 |
| 500KB             | 500ms              | ❌                    | --                                                                                                              | --                    | --                                 |
| 1000KB            | 50ms               | ✅                    | When 5 sync tabs are running, the longer they run, the higher the CPU usage becomes, until the browser crashes. | --                    | High frequency huge message test   |
| 1000KB            | 50ms               | ❌                    | --                                                                                                              | --                    | Continuous huge message test       |
| 1000KB            | 100ms              | ✅                    | --                                                                                                              | --                    | Balanced huge message test         |
| 1000KB            | 100ms              | ❌                    | --                                                                                                              | --                    | Standard huge message test         |
| 1000KB            | 500ms              | ✅                    | --                                                                                                              | --                    | Low frequency huge message test    |
| 1000KB            | 500ms              | ❌                    | --                                                                                                              | --                    | Slow huge message test             |


