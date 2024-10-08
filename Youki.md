# Objective
**Build and Deploy Youki Container Runtime in Linux**

## Introduction
This journal documents the steps taken to set up Youki, a tool that helps run applications in containers. Containers are like small packages that include everything needed to run a program. We will also install Docker, which helps manage these containers.

---

### Task:
- Learn about Youki and all the needed software and tools which are used in the task.
- Install Rust (the programming language Youki is built with).
- Install Docker (a tool to manage containers).

---

### Step 1: Install Rust

1. **Open the Terminal:**
   - This is where we type commands for the computer to follow.

2. **Install Rust:**
   - Type this command and press Enter:
     ```bash
     curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
     ```
   - Follow the instructions on the screen.
3. **Configure your current shell**
   - Type this command, After configuring the shell, you can run Rust commands directly from the terminal without navigating to the installation 
      directory.
     
     ```bash
     source $HOME/.cargo/env
     ```
   
   - Now, Check if Rust is installed by typing:
     ```bash
     rustc --version
     ```
   - You should see the version number of Rust.

---
## Step 2: Install Docker

### What is Docker?
- Docker is a tool that helps developers create, run, and manage containers. Containers are lightweight, portable units that package an application and everything it needs to run—like libraries, dependencies, and configurations.

### Installation Steps for Docker on Ubuntu:

1. **Update the Package List:**
   - Open the Terminal and type:
     ```bash
     sudo apt-get update
     ```
   - This command checks for updates in the system's package list.

2. **Install Necessary Packages:**
   - Type this command:
     ```bash
     sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
     ```
   - This installs tools needed for Docker to work correctly.

3. **Add Docker’s Official GPG Key:**
   - Type the following command:
     ```bash
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     ```
   - This step ensures that your system trusts Docker's software.

- **Now checking Docker is installed properly or not**
    ```bash
    docker --version
    ```

---
## Step 3: Build Youki

### Task:
- Now, we will build Youki from its source code.

### Steps to Build Youki:

1. **Install Required Dependencies:**
   - Type this command:
     ```bash
     sudo apt-get install libseccomp-dev pkg-config build-essential
     ```

2. **Clone the Youki Repository:**
   - This means we will get the Youki code from the internet. Type:
     ```bash
     git clone https://github.com/containers/youki.git
     ```

3. **Change Directory to Youki Folder:**
   - Move to the Youki folder:
     ```bash
     cd youki
     ```

4. **Build Youki:**
   - Type this command to compile the code:
     ```bash
     cargo build --release
     ```
   - After this, you should see an executable file created.

---

## Step 4: Setting up Youki as a default runtime
### Task:
- Configure Docker to use Youki by default.

### Steps to Set Youki as Default:

1. **Edit Docker's Configuration File:**
   - Open the file for editing:
     ```bash
     sudo vim /etc/docker/daemon.json
     ```

2. **Add Youki as the Default Runtime:**
   - Add this code inside the file:
  ```json
      {
        "default-runtime": "youki",
           "runtimes": {
               "youki": {
         "path": "/usr/local/bin/youki"
        }
      }
}
 ```
   - Replace `/path/to/youki` with the actual path where Youki was built.

3. **Restart Docker:**
   - Type this command:
     ```bash
     sudo systemctl restart docker
     ```

---

## Step 5: Run a comtainer using Youki Runtime

### Task:
- Run a container using Youki.

### Steps to Pull and Run a Container:

1. **Pull an Image from Docker Hub:**
   - This downloads a small version of a program. Type:
     ```bash
     docker pull alpine
     ```

2. **Run a Container Using Youki:**
   - Start a container using the command:
     ```bash
     docker run --rm -it alpine
     ```

---
## Step 6: Ensuring that the images which is pulled is using runtime Youki.
```bash
docker inspect CONTAINER_ID | grep -i "runtime"

```
**For checking container id we can use**
```bash
docker ps
```

## Step 7: Checking default runtime .
```bash
docker info | grep -i runtime
```
---

## Conclusion
- Youki has been successfully installed and set as the default runtime for Docker.
- I tested it by running a container, and it worked well.

This journal captures all the steps taken to set up Youki in simple terms. Feel free to ask if you have any questions or need more help!
