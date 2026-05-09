<p align="center">
<img width="1200" height="627" alt="image" src="https://github.com/user-attachments/assets/dd71265a-5862-4ed2-a198-804a50e00b22" />
</p>

<h1>Active Directory — Configuring Account Lockout Policy with Group Policy</h1>
This project demonstrates how to configure an Account Lockout Policy in Active Directory using the Group Policy Management Console (GPMC). This is a critical security configuration in any domain environment that protects against brute-force password attacks.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines / Compute)
- Remote Desktop Protocol (RDP)
- Active Directory Domain Services (AD DS)
- Group Policy Management Console (GPMC)
- Windows Server 2022

<h2>Operating Systems Used</h2>

- Windows Server 2022 (DC-1)
- Windows 10 Pro (21H2) (Client-1)

<h2>High-Level Steps</h2>

1. Open the Group Policy Management Console
2. Create a new Group Policy Object (GPO)
3. Configure Account Lockout Policy settings
4. Link the GPO to the domain
5. Force a Group Policy update
6. Verify the policy applied correctly

---

<h2>Step 1 — Open the Group Policy Management Console</h2>

<p>
<img width="1319" height="901" alt="image" src="https://github.com/user-attachments/assets/c42393aa-0f74-475a-a7ab-7defa9d3680e" />
</p>
<p>
I logged into DC-1 as mydomain.com\jane_admin and pressed Windows + R, typed gpmc.msc, and pressed Enter. This opened the Group Policy Management Console, where all domain-wide and OU-level policies are created and managed.
</p>
<br />

---

<h2>Step 2 — Create a New Group Policy Object</h2>

<p>
<img width="980" height="636" alt="image" src="https://github.com/user-attachments/assets/d5592092-8042-409b-ac3b-6a5ac85fa34c" />
</p>
<p>
In the left pane, I expanded the domain and right-clicked Group Policy Objects then selected New. I named the new GPO Account Lockout Settings. After creating it, I right-clicked the GPO and selected Edit to open the Group Policy Management Editor.
</p>
<br />

---

<h2>Step 3 — Configure Account Lockout Policy Settings</h2>

<p>
<img width="1467" height="617" alt="image" src="https://github.com/user-attachments/assets/3627d649-1f42-4a6a-9e73-ca3c2923740d" />
</p>
<p>
Inside the editor, I navigated to Computer Configuration, then Policies, then Windows Settings, then Security Settings, then Account Policies, and finally Account Lockout Policy. I configured the following three settings:
</p>

<p>
<img width="542" height="112" alt="image" src="https://github.com/user-attachments/assets/0e72e5f1-b1fc-46b5-a573-3e335ecfa7ae" />
</p>

| Setting | Value | Purpose |
|---|---|---|
| Account Lockout Threshold | 5 attempts | Locks account after 5 wrong passwords |
| Account Lockout Duration | 30 minutes | Account stays locked for 30 minutes |
| Reset Lockout Counter After | 15 minutes | Failed attempt counter resets after 15 minutes |

<p>
For each setting I double-clicked it, checked Define this policy setting, and entered the value.
</p>
<br />

---

<h2>Step 4 — Link the GPO to the Domain</h2>

<p>
<img width="1691" height="927" alt="image" src="https://github.com/user-attachments/assets/bcb87a8a-33af-4585-a776-0d705f98c241" />
</p>
<p>
Back in the GPMC, I right-clicked the domain mydomain.com and selected Link an Existing GPO. I selected the Account Lockout Settings GPO and clicked OK. Linking the GPO to the domain applies it to all users and computers within the domain.
</p>
<br />

---

<h2>Step 5 — Force a Group Policy Update</h2>

<p>
<img width="980" height="511" alt="image" src="https://github.com/user-attachments/assets/390ecbdd-821a-4320-8db7-5659a7913ab2" />
</p>
<p>
Rather than waiting for the policy to propagate automatically, I opened Command Prompt on Client-1 and ran gpupdate /force. This immediately pulled and applied the latest Group Policy settings from the domain controller.
</p>
<br />

---

<h2>Step 6 — Verify the Policy Applied</h2>

<p>
<img width="964" height="552" alt="image" src="https://github.com/user-attachments/assets/553fa065-7c74-40fc-857a-b9b5df6e3330" />
</p>
<p>
To confirm the policy was applied correctly, I ran rsop.msc on Client-1. The Resultant Set of Policy tool showed the Account Lockout Policy settings were active and matched the values configured in the GPO — 5 attempts, 30 minute lockout, and a 15 minute reset counter.
</p>
<br />

---

<h2>Conclusion</h2>

An Account Lockout Policy is now enforced across the domain via Group Policy. Any account that exceeds 5 failed login attempts will be locked for 30 minutes, protecting the environment against brute-force attacks. This is a foundational security configuration in any Active Directory domain environment.
