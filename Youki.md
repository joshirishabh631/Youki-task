# Implementation Journal: Youki Container Runtime on HP EliteBook 820 G3

## Day 1: Understanding Youki and Setting Up

### Task:
- Learn about **Youki**, a container runtime written in **Rust**, and set up my laptop for it.
- Install:
  - **Rust** (to build Youki)
  - **Docker** (to compare and use with Youki)

---

## Step 1: Install Rust

### What is Rust?
- **Rust** is a programming language needed to compile Youki, as it is written in Rust.

### Installation Steps for Rust:
1. Open your terminal.
2. Run the following command to install Rust:
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```
**Follow the on-screen instructions to install Rust**
**After installation, verify the installation by checking the version**
```bash
rustc --version
``` 
