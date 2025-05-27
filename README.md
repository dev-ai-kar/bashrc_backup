# 🚀 **README: `.bashrc_backup` Management & Git Workflow**

### **1️⃣ Backup & Version Control**
```bash
cd ~/.bashrc_backup
cp ~/.bashrc ~/.bashrc_backup
git diff
git commit -am "Updated .bashrc with nvm activation"
```

Manually added section for better organization, readability, and personalization:
```bash
# ✨ BEGIN Vaibhav’s Custom Config ✨
conda activate pyvenv_3.13
# 🔥 END Vaibhav’s Custom Config 🔥
```
---

## **2️⃣ Purpose of `.bak` Files for Local Backup**
A `.bak` file serves as a **backup file**, storing previous versions of configurations to prevent accidental corruption or loss.

### **Where `.bak` Files Are Used:**
- **Configuration Files** → Before modifying `.bashrc`, `.vimrc`, users often create a `.bak` version (`~/.bashrc.bak`).
- **Databases** → SQL databases generate `.bak` files for safe rollback.
- **Software & Games** → Some applications auto-create `.bak` versions.
- **Programming Projects** → Developers manually create backups before making risky changes.

### **Example Usage in Bash**
Create a backup before editing:
```bash
cp ~/.bashrc ~/.bashrc.bak
```
Restore if needed:
```bash
mv ~/.bashrc.bak ~/.bashrc
```

---

## **3️⃣ Git Workflow & Authentication Methods for Remote backups**
### **🔹 Recommended Authentication Methods**
#### ✅ **1. SSH (Most Secure & Convenient)**
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- Add the key to GitHub at: [GitHub SSH Keys](https://github.com/settings/keys)
- Update Git remote:
  ```bash
  git remote set-url origin git@github.com:yourusername/bashrc_backup.git
  ```
- Pull/push **without needing credentials**:
  ```bash
  git pull origin main
  git push origin main
  ```

#### ✅ **2. Personal Access Token (PAT) with HTTPS**
- Generate a token: [GitHub Tokens](https://github.com/settings/tokens)
- Use it instead of a password:
  ```bash
  git pull https://github.com/yourusername/bashrc_backup.git
  git push https://github.com/yourusername/bashrc_backup.git
  ```

📌 **SSH is recommended** for security and automation.

---

## **4️⃣ Git Branching Strategies**
### **Core Branches**
| **Branch**  | **Purpose** |
|-------------|------------|
| `main` | Primary stable branch. |
| `develop` | Integration branch for new features. |

### **Feature-Specific Branches**
| **Branch**  | **Purpose** |
|-------------|------------|
| `feature/*` | Individual development branches. |
| `hotfix/*` | Emergency fixes for production. |
| `release/*` | Pre-release testing before deployment. |
| `staging` | Mirrors production for testing. |
| `prod` | The final, stable branch for deployment. |

A **dedicated `prod` branch** ensures stability before production deployment.

---

## **5️⃣ Conda Environment & `.bashrc` Customization**
### **Auto-Activate `pyvenv_3.13` on Terminal Startup**
Modify `~/.bashrc`:
```bash
echo "conda activate pyvenv_3.13" >> ~/.bashrc
source ~/.bashrc
```

### **List Conda Environments on Terminal Startup**
```bash
echo "Available Conda Environments:"
conda env list | awk '{print $1}' | grep -v '^#' | while read env; do
    echo -n "$env: "
    conda run -n "$env" python --version 2>/dev/null || echo "No Python installed"
done
```

This prints Conda environments along with their Python versions.

To **set `pyvenv_3.13` as your default Conda environment**, follow these steps:

### **1. Disable Auto-Activation of `base`**
By default, Conda activates the `base` environment. To prevent this:
```bash
conda config --set auto_activate_base false
```

### **2. Automatically Activate `pyvenv_3.13` on Startup**
Edit your shell configuration file (`.bashrc`, `.zshrc`, etc.):

```bash
echo "conda activate pyvenv_3.13" >> ~/.bashrc
source ~/.bashrc
```
This ensures `pyvenv_3.13` is activated whenever you open a new terminal.

### **3. List All Conda Environments**
To see all available Conda environments, run:
```bash
conda env list
```
or
```bash
conda info --envs
```
Your active environment will be marked with `*`.

Let me know if you need further tweaks! 🚀 You can also check out [Conda's official documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) for more details.

To create a **Miniconda virtual environment** named `venv_3.12` using the **latest Python version**, follow these steps:

### **1. Update Conda**
First, ensure Conda is up to date:
```bash
conda update -n base -c defaults conda
```

### **2. Create the Virtual Environment**
Run this command to create `venv_3.12` with the latest Python version:
```bash
conda create -n venv_3.12 python
```
By default, Conda will install the latest available Python version.

### **3. Activate the Environment**
Once created, activate it with:
```bash
conda activate venv_3.12
```

### **4. Verify Python Version**
Check the installed Python version inside the environment:
```bash
python --version
```

If you need a **specific Python version**, you can specify it during creation:
```bash
conda create -n venv_3.12 python=3.12
```

Let me know if you need help configuring dependencies or optimizing your setup! 🚀 You can also check out [Conda's official documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) for more details.

---

## **6️⃣ Setting Up Node.js & NVM**
### **Check Node.js Version**
```bash
node -v
```

### **Install Node.js (If Missing)**
```bash
sudo apt update
sudo apt install nodejs
```

### **Install & Use NVM for Node.js Version Management**
```bash
curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
source ~/.bashrc
nvm install 18
nvm use 18
```
