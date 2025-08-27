# 🚀 BroadcastChannel Multi-Tab Performance Test

> A comprehensive performance testing suite for the browser BroadcastChannel API, designed to evaluate message transmission performance across different scenarios and configurations.

## 📋 Project Overview

BroadcastChannel API is a Web standard that enables communication between different tabs, iframes, or workers within the same origin. This project provides multiple test scenarios to assess its real-world performance characteristics, including latency, throughput, and scalability metrics.

## 🧪 Test Components

| Component                                                         | Purpose                 |
| ----------------------------------------------------------------- | ----------------------- |
| **`index.html`**                                                  | Test Suite Navigation   |
| **`basic-performance-test.html`**                                 | Basic Performance Test  |
| **`publisher.html`**                                              | Message Publisher       |
| **`customer-sync.html`**                                          | Consumer with Sync      |
| **`customer-no-sync.html`**                                       | Independent Consumer    |

## 🚀 Quick Start

1. **Open the main page**: Navigate to `index.html` to see all available test components
2. **Choose your test**: Click on any test card to open the specific testing tool
3. **Run tests**: Follow the instructions in each test component
4. **Compare results**: Use different components to test various scenarios

## 📋 Test Component Details

### **Basic Performance Test** (`basic-performance-test.html`)

- Simple multi-tab communication test
- Measures latency across different message sizes
- Good for initial performance assessment

### **Message Publisher** (`publisher.html`)

- Configurable message publishing
- Adjustable size (10KB - 1000KB) and speed (50ms - 500ms)
- Publishing history and statistics

### **Consumer with Sync** (`customer-sync.html`)

- Cross-tab data synchronization
- Real-time performance metrics
- Request-response messaging mode

### **Independent Consumer** (`customer-no-sync.html`)

- Standalone consumer for isolated testing
- Same features with Consumer Sync
- Useful for sync overhead comparison

## ⚠️ Background Tab Throttling

> **🚨 Critical Finding**: When the publisher tab is in the background, browser throttling will **dramatically reduce performance by 10x or more**.

**📊 Performance Impact Example**: 
In the High frequency medium message test (100KB message size, 50ms publish speed), the messages per second count drops from **20 to 2-3** when the publisher tab is in the background.

### **💡 Key Conclusions**:

> **🎯 Main Takeaway**: Background tab throttling can reduce message throughput by **90% or more**
> 
> **⚡ Performance Drop**: From 20 msg/sec → 2-3 msg/sec (10x reduction)
> 
> **🔧 Root Cause**: Browser timer throttling, not BroadcastChannel API limitations


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

## 🤖 AI Development Process

This test suite was developed using AI assistance. We started with a real-world project scenario where we needed to test BroadcastChannel performance, and had some initial metrics in mind (like message delivery latency). Through open-ended questions, we developed a much more comprehensive performance testing framework.

**🚀 Development Speed**: Thanks to Cursor AI assistance, this entire test suite was completed in under 30 minutes! While the code wasn't perfectly clean, Cursor quickly identified and fixed all the bugs according to requirements, demonstrating impressive development efficiency. 

Here are the key prompts that guided the development process:

### **🔍 Initial Questions**
- "Help me build a customer and publisher to test BroadcastChannel API performance"
- "I also want a customer with tab sync functionality, build one for me"

### **🧪 Testing Strategy Development**
- "What test scenarios would be most valuable for understanding BroadcastChannel performance?"
- Then some human work to test and adjust the testing strategy

These open-ended questions helped explore the problem space without assuming specific solutions. What started as a simple latency test evolved into a comprehensive framework that covers message size impact, frequency variations, consumer architectures, and browser behavior insights - revealing performance characteristics we hadn't initially considered.

## 📚 Additional Resources

- [BroadcastChannel API Documentation](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel)
- [Heavy throttling of chained JS timers beginning in Chrome 88](https://developer.chrome.com/blog/timer-throttling-in-chrome-88)
- [How to Enable and Disable Google Chrome Background Tab Throttling in Windows (But the solution is not working)](https://www.ninjaone.com/blog/configure-background-tab-throttling-chrome/)
