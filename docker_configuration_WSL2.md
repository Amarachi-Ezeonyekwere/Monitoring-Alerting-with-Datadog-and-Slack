# Installing Docker in WSL2 without Docker Desktop

This guide documents the step-by-step installation of Docker inside **WSL2 Ubuntu**, without relying on Docker Desktop. It includes setup, troubleshooting, and verification.

---

##  Step 1: Verify WSL2 Installation
Run the following command in **PowerShell** to list installed distros and check WSL version:


```powershell
wsl -l -v
```

Example output:
```
  NAME      STATE           VERSION
* Ubuntu    Stopped         2
```

Ensure that your distro (e.g., `Ubuntu`) is set to **version 2**. 
If not, run:

```powershell
wsl --set-version <YourDistroName> 2
```

---

##  Step 2: Open Ubuntu in WSL2
Launch **Ubuntu** from Start Menu or **Windows Terminal**.

> ⚠️Copy-paste tip: 
> - In Ubuntu window - use **Right-click** or **Ctrl+Shift+V** to paste. 
> - In Windows Terminal - **Ctrl+V** works normally.

---

##  Step 3: Update Package Index
Inside Ubuntu, run:

```bash
sudo apt update && sudo apt upgrade -y
```

---

##  Step 4: Install Required Packages
```bash
sudo apt-get install ca-certificates curl gnupg lsb-release -y
```

---

##  Step 5: Add Docker’s Official GPG Key
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

---

##  Step 6: Set Up Docker Repository
```bash
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update apt again:
```bash
sudo apt update
```

---

##  Step 7: Install Docker Engine
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```

---

##  Step 8: Run Docker Without `sudo` (Optional but Recommended)
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

Logout and re-open Ubuntu for changes to take effect.

---

##  Step 9: Test Docker Installation
Run the test image:
```bash
docker run hello-world
```

Expected output:
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

---

#   Troubleshooting notes to some challenges I encountered.

###   Problem: `sudo` not recognized in PowerShell
- Solution: Commands with `sudo` must be run **inside Ubuntu WSL**, not PowerShell.

###   Problem: Cannot paste into Ubuntu terminal
- Solution: 
  - Use **Ctrl+Shift+V** (not Ctrl+V). 
  - Or install **Windows Terminal** for easier paste. 


---

#  Final Verification
```bash
dock run hello-world
```
Confirmes : Docker installed successfully inside WSL2 Ubuntu **without Docker Desktop**.
