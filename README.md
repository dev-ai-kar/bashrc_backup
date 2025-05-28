# 🚀 **`terminal-setup` Management & Git Workflow**

### **1️⃣ Backup & Version Control**
```bash
cd ~/terminal-setup 
cp ~/.bashrc ~/terminal-setup
# VS Code Settings - /C:/Users/vaibh/AppData/Roaming/Code/User/settings.json
cp /mnt/c/users/vaibh/AppData/Roaming/Code/User/settings.json ~/terminal-setup/windows_terminal_settings.json
# Windows Terminal Settings - C:\Users\vaibh\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json
cp /mnt/c/users/vaibh/AppData/Local/Packages/Microsoft.WindowsTerminal_8wekyb3d8bbwe/LocalState/settings.json ~/terminal-setup/windows_terminal_settings.json
cp /home/deokar/.config/oh-my-posh/my-custom-theme.json ~/terminal-setup/oh-my-posh/my-custom-theme.json
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
  git remote set-url origin git@github.com:yourusername/terminal-setup.git
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
  git pull https://github.com/yourusername/terminal-setup.git
  git push https://github.com/yourusername/terminal-setup.git
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

To create a **Miniconda virtual environment** named `pyvenv_3.13` using the **latest Python version**, follow these steps:

### **1. Update Conda**
First, ensure Conda is up to date:
```bash
conda update -n base -c defaults conda
```

### **2. Create the Virtual Environment**
Run this command to create `pyvenv_3.13` with the latest Python version:
```bash
conda create -n pyvenv_3.13 python
```
By default, Conda will install the latest available Python version.

### **3. Activate the Environment**
Once created, activate it with:
```bash
conda activate pyvenv_3.13
```

### **4. Verify Python Version**
Check the installed Python version inside the environment:
```bash
python --version
```

If you need a **specific Python version**, you can specify it during creation:
```bash
conda create -n pyvenv_3.13 python=3.12
```

You can also check out [Conda's official documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) for more details.

### **Auto-Activate `pyvenv_3.13` on Terminal Startup**
Modify `~/.bashrc`:
```bash
echo "conda activate pyvenv_3.13" >> ~/.bashrc
source ~/.bashrc
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

### **List Conda Environments on Terminal Startup**
```bash
echo "Available Conda Environments:"
conda env list | awk '{print $1}' | grep -v '^#' | while read env; do
    echo -n "$env: "
    conda run -n "$env" python --version 2>/dev/null || echo "No Python installed"
done
```

Let me know if you need further tweaks! 🚀 You can also check out [Conda's official documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) for more details.

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

## **7️⃣ Linux terminal animations and ASCII art tools**
Combining `fortune`, `cowsay`, and `lolcat` creates a colorful, witty message every time you open your terminal. Here’s how you can set it up:

### 1️⃣ Install the Required Packages
Make sure you have all three installed:
```bash
sudo apt install fortune cowsay lolcat  # Debian/Ubuntu
sudo yum install fortune-mod cowsay lolcat  # CentOS/RHEL
sudo pacman -S fortune cowsay lolcat  # Arch Linux
```

### 2️⃣ Add This to Your `.bashrc` File
Edit your `.bashrc` and insert this snippet at the end:
```bash
fortune | cowsay | lolcat
```

### 3️⃣ Save & Apply Changes
Run:
```bash
source ~/.bashrc
```

### 🎉 Now, Every Time You Open Your Terminal…
You’ll see a **random fortune**, spoken by a **cute ASCII cow**, with **rainbow colors**! 🌈🐮✨

Want to make it even fancier? You could wrap it in a function to randomize cows:
```bash
function random_cow_fortune() {
    fortune | cowsay -f $(ls /usr/share/cowsay/cows | shuf -n 1) | lolcat
}
random_cow_fortune
```
This will make the cow **change species** every time! 🐱🐧🐸

You can add dragons, penguins, sheep, and a bunch of other creatures to your **fortune + cowsay + lolcat** setup. 🐲🐧🐑

### **1️⃣ Check Available Characters**
Cowsay supports multiple “cows” (actually, different ASCII creatures). You can see all available characters by running:
```bash
ls /usr/share/cowsay/cows
```
You’ll find options like:
- `dragon.cow` 🐲 (Epic!)
- `penguin.cow` 🐧
- `elephant.cow` 🐘
- `sheep.cow` 🐑
- `tux.cow` 🐧 (Linux mascot)
- And more!

### **2️⃣ Randomize Your ASCII Creatures**
Edit your `.bashrc` and replace your existing command with:
```bash
fortune | cowsay -f $(ls /usr/share/cowsay/cows | shuf -n 1) | lolcat
```
This makes **a different creature** deliver your fortune every time you open the terminal! 🦄✨

### **3️⃣ Save & Apply Changes**
```bash
source ~/.bashrc
```
Now, every time you open your terminal, a **random animal or dragon** will appear with a colorful message. 🔥🐲


You can modify your function to **randomly choose** between different outputs—fortune, Node.js version, npm version, and available Conda environments. Here's an improved version of your function:

```bash
function random_cow_message() {
    case $((RANDOM % 4)) in
        0) fortune ;;
        1) echo "Node.js Version: $(node -v)" ;;
        2) echo "npm Version: $(npm -v)" ;;
        3) echo "Available Conda Environments:" && conda env list ;;
    esac | cowsay -f $(ls /usr/share/cowsay/cows | shuf -n 1) | lolcat
}

random_cow_message
```

### 🔥 How It Works:
1. **Uses `$((RANDOM % 4))`** to randomly pick one of four outputs:
   - A fortune 🦄
   - Node.js version 🔧
   - npm version 📦
   - List of available Conda environments 🔥
2. **Pipes the result into `cowsay`**, randomizing the ASCII creature.
3. **Adds colorful output with `lolcat`** for flair.

Now, whenever you open your terminal, you’ll get a **random message from a random creature** in beautiful colors! 🌈🐲🐧🐑 

Let me know if you want more tweaks! 🚀😄

