# Task 4: Atomic Red Team Execution & Detection Report

## Environment Setup
*   **Environment:** Windows Host Machine (Manual Simulation)
*   **Logging:** Sysmon (Event ID 1) & Windows Security Logs
*   **Note:** Because the environment lacked a dedicated VM, the specific commands executed by Atomic Red Team were run manually to simulate the techniques and generate telemetry.

---

## 1. Technique: T1059.001 (PowerShell)
*   **Atomic Name:** Mimic Malicious PowerShell Command
*   **Execution Command:** `powershell.exe -Command "Write-Host 'Atomic Test T1059.001 Execution'"`
*   **Sysmon Events Generated:** **Event ID 1 (Process Create)**
    *   **Key Fields:** 
        *   `Image:` `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`
        *   `CommandLine:` `"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe"` (or the specific command executed).
*   **SIEM Evidence:** N/A (Logs reviewed directly in Event Viewer).
*   **Did an alert fire?** No.
*   **Detection Gap Identified:** The environment lacks a SIEM rule to alert on PowerShell execution, especially with suspicious flags like `-ExecutionPolicy Bypass` or `-NoProfile`.
*   **Screenshot:** `Findings/Task No 4/T1059_Sysmon.png`

---

## 2. Technique: T1136.001 (Create Local Account)
*   **Atomic Name:** Create a local user account using cmd
*   **Execution Command:** `net user TestUser P@ssw0rd /add`
*   **Sysmon Events Generated:** **Windows Security Event ID 4720 (User Account Created)**
    *   **Key Fields:** 
        *   `New Account Name:` `TestUser`
        *   `Subject Account Name:` `karan` (The user who executed the command)
        *   `Computer:` `windows-11`
*   **SIEM Evidence:** N/A
*   **Did an alert fire?** No.
*   **Detection Gap Identified:** We need an alert for local user creation (Event ID 4720). Adversaries often create local accounts for persistence and lateral movement.
*   **Screenshot:** `Findings/Task No 4/T1136_Event4720.png`

---

## 3. Technique: T1053.005 (Scheduled Task)
*   **Atomic Name:** Scheduled Task Startup Script
*   **Execution Command:** `schtasks /create /tn "TestTask" /tr "calc.exe" /sc onlogon`
*   **Sysmon Events Generated:** **Event ID 1 (Process Create)**
    *   **Key Fields:** 
        *   `Image:` `C:\Windows\System32\schtasks.exe`
        *   `CommandLine:` `schtasks /create /tn "TestTask" /tr "calc.exe" /sc onlogon`
*   **SIEM Evidence:** N/A
*   **Did an alert fire?** No.
*   **Detection Gap Identified:** We lack a detection rule for persistence via Scheduled Tasks. We should alert when `schtasks.exe` is used with the `/create` flag, especially if it points to suspicious binaries.
*   **Screenshot:** `Findings/Task No 4/T1053_Sysmon.png`