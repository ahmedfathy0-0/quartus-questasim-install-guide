
# 📘 Installation Guide for Quartus Prime & QuestaSim on Linux (Arch / Fedora / Ubuntu)

This guide explains how to install **Intel Quartus Prime Lite** (for FPGA development) and **QuestaSim** (for VLSI simulation) on Linux.  
It also includes license setup instructions to avoid common issues.

---

## 🔗 Official Download Links

- **Quartus Prime Lite (Linux, v24.1)**  
  [Intel Quartus Prime Lite Edition v24.1 Download](https://www.intel.com/content/www/us/en/software-kit/849769/intel-quartus-prime-lite-edition-design-software-version-24-1-for-linux.html)

- **Questa Intel FPGA Edition (Linux, v25.1.1)**  
  [Intel Questa FPGA Edition v25.1.1 Download](https://www.intel.com/content/www/us/en/software-kit/862384/questa-intel-fpgas-pro-edition-software-version-25-1-1.html)

- **License Instructions PDF (look at part 2)**  
  [University of Florida QuestaSim & Quartus License Guide](https://mil.ufl.edu/3701/docs/quartus/QuestaSim_with_Quartus21.pdf)

---

## ⚙️ 1. Install Quartus Prime Lite

1. Download the `.run` file from Intel’s website.
2. Make it executable:
   ```bash
   chmod +x QuartusLiteSetup-24.1.0.109.run
   ```
3. Run installer:
   ```bash
   ./QuartusLiteSetup-24.1.0.109.run
   ```
4. Follow the GUI installer and select installation path (default: `/home/$USER/intelFPGA_lite/24.1`).

---

## ⚙️ 2. Install QuestaSim

1. Download the `.run` file from Intel.
2. Make it executable:
   ```bash
   chmod +x QuestaSetup-25.1.1.44.run
   ```
3. Run installer with root (recommended to install under `/root/altera_pro/`):
   ```bash
   sudo ./QuestaSetup-25.1.1.44.run
   ```
4. Default path:  
   ```
   /root/altera_pro/25.1.1/questa_fse
   ```

---

## 🔑 3. License Setup

You need a **license file (`license.dat` or `LR-xxxxx_License`)**.

1. Generate a license at Intel’s licensing portal:
   - When asked for **Computer Type**, choose:
     - `NIC` (Network Interface Card) → then enter your **MAC Address**  
       - Find MAC address:
         ```bash
         ip addr show
         ```
         Look for `ether xx:xx:xx:xx:xx:xx`
   - The license file will be emailed or downloaded as `LR-XXXXX_License.dat`.

2. Place the license file in a known location (e.g. `/root/altera_pro/license.dat`).

3. Set environment variable:
   ```bash
   export LM_LICENSE_FILE=/root/altera_pro/license.dat
   ```
   Add it permanently to your shell:
   - For **bash/zsh**:
     ```bash
     echo 'export LM_LICENSE_FILE=/root/altera_pro/license.dat' >> ~/.bashrc
     source ~/.bashrc
     ```

4. Verify environment:
   ```bash
   echo $LM_LICENSE_FILE
   ```
   Should return:
   ```
   /root/altera_pro/license.dat
   ```

---

## ▶️ 4. Running QuestaSim

1. Start QuestaSim:
   ```bash
   /root/altera_pro/25.1.1/questa_fse/bin/vsim
   ```
2. If you see:
   ```
   Unable to find the license file.
   ```
   → Ensure `LM_LICENSE_FILE` is exported correctly.

---

## ✅ Quick Checklist Before Running

- [ ] Installed Quartus & QuestaSim correctly.  
- [ ] License file (`license.dat`) exists in `/root/altera_pro/`.  
- [ ] `LM_LICENSE_FILE` is exported in `~/.bashrc`.  
- [ ] MAC address used for license matches the current machine.  
- [ ] Run QuestaSim as:
  ```bash
  vsim
  ```
  or full path:
  ```bash
  /root/altera_pro/25.1.1/questa_fse/bin/vsim
  ```

---

## 📌 Notes for Arch Users

- Make sure to install `libxft`, `libxext`, and other 32-bit dependencies:
  ```bash
  sudo pacman -S libxft libxext lib32-glibc lib32-libx11 lib32-libxft
  ```

- Fedora/Ubuntu users may need:
  ```bash
  sudo dnf install libXft libXext
  sudo apt install libxft2 libxext6
  ```

---

## 🎯 Final Advice

- Keep your license file backed up.  
- Share this guide with others to avoid issues with `license.dat` path and environment variables.  
- Always test with:
  ```bash
  vsim
  ```
  to confirm the license works.
