# Implementation Journal: Youki Container Runtime on HP EliteBook 820 G3

## Day 1: Understanding Youki and Setting Up

### Task:
- Learn about **Youki**, which is a container runtime like **Docker** but written in **Rust**.
- Plan to build and use Youki on my laptop.

### Steps Taken:
- I researched what Youki is and its benefits. 
- I set up my HP EliteBook 820 G3 for Youki by installing the necessary tools:
  - Rust (because Youki is written in Rust)
  - Docker (for comparison and testing)

### Issues Faced:
- It was a bit confusing to understand how Youki works differently from Docker.

### Solution:
- I read more about container runtimes and how they handle containers.

---

## Day 2: Building and Installing Youki

### Task:
- Build and install Youki from its source code.

### Steps Taken:
1. Cloned the Youki code from GitHub:
    ```bash
    git clone https://github.com/containers/youki.git
    ```
2. Built the code using Rust:
    ```bash
    cd youki
    cargo build --release
    ```

- The build process created the **Youki executable**.

### Issues Faced:
- The build took some time because it's compiling everything from scratch.

### Solution:
- I waited patiently for it to complete and kept checking for errors.

---

## Day 3: Setting Youki as Default Runtime in Docker

### Task:
- Make **Youki** the default container runtime instead of Docker's default.

### Steps Taken:
1. Modified the Docker daemon configuration:
    ```bash
    sudo nano /etc/docker/daemon.json
    ```

2. Added Youki as the default runtime:
    ```json
    {
      "runtimes": {
        "youki": {
          "path": "/path/to/youki"
        }
      },
      "default-runtime": "youki"
    }
    ```

3. Restarted Docker:
    ```bash
    sudo systemctl restart docker
    ```

### Issues Faced:
- Initially, Docker wouldn't restart properly because I misconfigured the path.

### Solution:
- I checked the correct location of the Youki binary and fixed the path.

---

## Day 4: Pulling and Running a Container with Youki

### Task:
- Test **Youki** by pulling and running a container.

### Steps Taken:
1. Pulled an image from Docker Hub:
    ```bash
    docker pull alpine
    ```

2. Created and ran a container using Youki:
    ```bash
    docker run --rm -it alpine
    ```

- The container ran successfully with Youki as the runtime.

### Issues Faced:
- No major issues today, everything worked fine!

### Outcome:
- Successfully used Youki to run a container on my system.
