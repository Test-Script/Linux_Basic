Run levels in Linux define the state of the operating system and control what services or processes are running. They determine whether the system operates in **single-user mode**, **multi-user mode**, or **graphical mode**, among others. Traditional **SysVinit** systems use run levels, while modern **Systemd** replaces them with **targets**, which offer similar functionality but are more flexible.

---

### **Run Levels in SysVinit**

| **Run Level** | **Description**                                    | **System State**                          |
|---------------|----------------------------------------------------|-------------------------------------------|
| **0**         | Halt/Shutdown                                      | The system is stopped and powered off.    |
| **1**         | Single-user mode                                   | Minimal mode for maintenance (no network).|
| **2**         | Multi-user mode (without NFS/networking services)  | Rarely used in most distributions.        |
| **3**         | Full multi-user mode                               | Command-line only (no GUI).               |
| **4**         | Unused/Custom                                      | Reserved for custom configurations.       |
| **5**         | Multi-user mode with GUI                           | Graphical desktop environment.            |
| **6**         | Reboot                                             | The system reboots.                       |

---

### **How to Check and Change Run Levels**

#### 1. **Check Current Run Level**
   - Use the `runlevel` command:
     ```bash
     runlevel
     ```
     - Output example: `N 3`  
       - `N` indicates there was no previous run level.
       - `3` indicates the current run level.

#### 2. **Change Run Level**
   - Use the `init` or `telinit` command:
     ```bash
     init <runlevel>
     ```
     Example: To switch to run level 5 (GUI mode):
     ```bash
     init 5
     ```

---

### **Run Levels in Systemd**

In **Systemd**, run levels are replaced by **targets**, which are more versatile and provide the same functionality.

| **Run Level** | **Systemd Target**           | **Description**                          |
|---------------|------------------------------|-------------------------------------------|
| **0**         | `poweroff.target`           | Halt/Shutdown.                            |
| **1**         | `rescue.target`             | Single-user mode.                         |
| **2, 3, 4**   | `multi-user.target`         | Full multi-user mode (command-line only). |
| **5**         | `graphical.target`         | Multi-user mode with GUI.                 |
| **6**         | `reboot.target`            | Reboots the system.                       |

#### **How to Check and Change Targets in Systemd**
1. **Check Current Target**:
   ```bash
   systemctl get-default
   ```
   Example Output: `multi-user.target`

2. **Change Target Temporarily**:
   - Switch to a different target (e.g., graphical):
     ```bash
     systemctl isolate graphical.target
     ```

3. **Set Default Target**:
   - To make a target the default at boot:
     ```bash
     systemctl set-default graphical.target
     ```
   - Verify the change:
     ```bash
     systemctl get-default
     ```

---

### **Comparison: Run Levels vs. Targets**

| **Feature**              | **Run Levels (SysVinit)**       | **Targets (Systemd)**         |
|---------------------------|----------------------------------|--------------------------------|
| Configuration Location    | `/etc/inittab`                 | `/etc/systemd/system/`        |
| Flexibility               | Fixed levels (0–6)             | Customizable targets.         |
| Dependency Handling       | No dependency management       | Handles service dependencies. |
| Examples                  | Run level 3, Run level 5        | `multi-user.target`, `graphical.target` |

---

### **Common Targets in Systemd**

- `rescue.target`: Single-user mode.
- `multi-user.target`: Multi-user command-line mode.
- `graphical.target`: Multi-user with graphical interface.
- `poweroff.target`: System shutdown.
- `reboot.target`: System reboot.
- `emergency.target`: Bare minimum mode (even fewer services than rescue).

---

If you need further assistance with managing run levels or targets, let me know!