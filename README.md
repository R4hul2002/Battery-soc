# VLSI Design Verification (DV) Interview Questions & Answers

---

## **1. Basics of Verification**

### **Q1. What is the difference between verification and validation?**
- **Verification** checks if the design meets specifications (e.g., "Did we build the design right?").  
- **Validation** ensures the design meets user needs (e.g., "Did we build the right design?").  
- **Example**:  
  - Verification: Checking if an adder circuit correctly adds two numbers.  
  - Validation: Ensuring the adder works in the target system (e.g., a CPU).  

### **Q2. Explain the Verification Lifecycle in VLSI.**
1. **Requirement Analysis** – Define test goals.  
2. **Test Planning** – Develop test strategies (directed/random).  
3. **Testbench Development** – UVM/SV testbench coding.  
4. **Test Execution** – Run simulations (RTL, gate-level).  
5. **Debugging** – Analyze failures.  
6. **Coverage Closure** – Ensure 100% functional/code coverage.  
7. **Sign-off** – Tape-out readiness.  

### **Q3. What are the different verification methodologies?**
- **UVM (Universal Verification Methodology)** – Most widely used (IEEE 1800.2).  
- **OVM (Open Verification Methodology)** – Predecessor to UVM.  
- **VMM (Verification Methodology Manual)** – Older, from Synopsys.  
- **eRM (e Reuse Methodology)** – Used with Specman.  

### **Q4. What is the role of a testbench in verification?**
- A **testbench** is a virtual environment that:  
  - Stimulates the **DUT (Design Under Test)**.  
  - Checks responses (via assertions/checkers).  
  - Measures coverage.  
- **Components**: Driver, Monitor, Scoreboard, Sequencer.  

### **Q5. Differences between simulation, emulation, and FPGA prototyping?**
| **Method**       | **Speed** | **Accuracy** | **Use Case**                     |
|------------------|----------|-------------|----------------------------------|
| Simulation       | Slow     | High         | RTL Debugging                    |
| Emulation        | Faster   | Medium       | Pre-silicon validation           |
| FPGA Prototyping | Fastest  | Low          | Software validation (near-real-time) |

---

## **2. SystemVerilog & UVM**

### **Q6. Key features of SystemVerilog for verification?**
- **OOP support** (classes, inheritance).  
- **Constrained Randomization** (`rand`, `randc`).  
- **Assertions (SVA)** – Formal checks.  
- **Covergroups** – Functional coverage.  
- **Interfaces** – Modular TB connections.  

### **Q7. Differences between `logic`, `wire`, and `reg`?**
- **`logic`** – 4-state (0,1,X,Z), replaces `reg`/`wire` in SV.  
- **`wire`** – Net type (used for structural connections).  
- **`reg`** – Legacy, holds value until reassigned.  

### **Q8. Differences between `always_comb`, `always_latch`, and `always_ff`?**
- **`always_comb`** – Combinational logic (auto-triggers on input changes).  
- **`always_latch`** – Explicit latch modeling.  
- **`always_ff`** – Flip-flop inference (clocked logic).  

### **Q9. Explain UVM architecture.**
![UVM Architecture](https://www.uvmworld.org/images/uvm_architecture.png)  
- **`uvm_test`** – Top-level test.  
- **`uvm_env`** – Testbench container.  
- **`uvm_agent`** – Driver/Monitor/Sequencer grouping.  
- **`uvm_sequence`** – Generates transactions.  
- **`uvm_driver`** – Sends transactions to DUT.  

### **Q10. What is `uvm_config_db`?**
- A **global database** to pass configuration settings (e.g., virtual interfaces).  
- **Example**:  
  ```systemverilog
  uvm_config_db#(virtual intf)::set(null, "*", "vif", intf);
  uvm_config_db#(virtual intf)::get(this, "", "vif", vif);
