<p align="center">
<img width="1200" height="627" alt="image" src="https://github.com/user-attachments/assets/dd71265a-5862-4ed2-a198-804a50e00b22" />


</p>

<h1>Configuring Account Lockout Policy in Active Directory</h1>
Here’s a step-by-step tutorial written to teach someone how to configure an Account Lockout Policy in Active Directory using Group Policy <br />



<h2>Environments and Technologies Used</h2>

- Virtualized Lab Environment
- Remote Desktop
- Active Directory Domain Services (AD DS)
- Windows Server 2022
- Networking Services

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>🔑 Prerequisites</h2>

- Two virtual machines: DC-1 → Windows Server 2022 (Domain Controller) Client-1 → Windows 10/11 or Server acting as a client
- You need access to a Windows Server that is a Domain Controller (DC).
- You must have the Group Policy Management Console (GPMC) installed.
- You should have permissions to create or edit Group Policy Objects (GPOs).
  

<h2>Account Lockout Policy in Active Directory using Group Policy</h2>

<p>
<img width="1319" height="901" alt="image" src="https://github.com/user-attachments/assets/c42393aa-0f74-475a-a7ab-7defa9d3680e" />


</p>
<p>
Open the Group Policy Management Console (GPMC)

Log in to a machine that has the GPMC installed (usually your Domain Controller). Click Start, type gpmc.msc in the search box, and press Enter. This opens the Group Policy Management Console.
</p>
<br />

<p>
<img width="980" height="636" alt="image" src="https://github.com/user-attachments/assets/d5592092-8042-409b-ac3b-6a5ac85fa34c" />


</p>
<p>
Create or Edit a Group Policy Object (GPO)

In the left-hand pane, expand your domain and find Group Policy Objects.

If you want a fresh policy:

Right-click Group Policy Objects → choose New.

Give it a clear name like “Account Lockout Settings”.

If you want to change an existing one:

Just right-click it → select Edit.
</p>
<br />

<p>
<img width="1467" height="617" alt="image" src="https://github.com/user-attachments/assets/3627d649-1f42-4a6a-9e73-ca3c2923740d" />


</p>
<p>
Navigate to the Account Lockout Policy Settings

In the Group Policy Management Editor, go to:
Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy.

</p>
<br />

</p>
<img width="542" height="112" alt="image" src="https://github.com/user-attachments/assets/0e72e5f1-b1fc-46b5-a573-3e335ecfa7ae" />


</p>
<p>

Set the Lockout Rules

Here’s where the real configuration happens. You’ll see three options:

Account Lockout Duration

How long accounts stay locked.

Example: 30 minutes.

Account Lockout Threshold

How many wrong password attempts before lockout.

Example: 3 tries.

Reset Account Lockout Counter After

How long until failed attempts reset back to zero.

Example: 15 minutes.

👉 To set each one, double-click it, check Define this policy setting, and enter your numbers.


</p>
<br />

</p>
<img width="1691" height="927" alt="image" src="https://github.com/user-attachments/assets/bcb87a8a-33af-4585-a776-0d705f98c241" />


</p>
<p>
  
Link the GPO to an Organizational Unit (OU)

In the GPMC, right-click the OU or domain where you want the policy applied.

Select Link an Existing GPO.

Choose the GPO you just created or modified → click OK.


</p> 
<br /> 

<p/>
<img width="980" height="511" alt="image" src="https://github.com/user-attachments/assets/390ecbdd-821a-4320-8db7-5659a7913ab2" />


</p>
<p>
Update Group Policy

Wait for Group Policy to propagate automatically, or force an immediate update:

Open Command Prompt on a client machine or server.

Type gpupdate /force and press Enter.

</p> 
<br /> 

<p/>
<img width="964" height="552" alt="image" src="https://github.com/user-attachments/assets/553fa065-7c74-40fc-857a-b9b5df6e3330" />


</p>
<p>
✅ Step 7: Check That It Worked

To confirm, you have two options:

Run rsop.msc on a client and look for the Account Lockout settings.

Or, use the Group Policy Results wizard in GPMC to check applied settings.


</p>
<p>
⚠️ Pro Tips

Don’t set the lockout threshold too low (like 1–2 attempts) — you’ll end up locking out users constantly.

Don’t make the lockout duration excessively long — balance convenience and security.

Resetting the counter after 15 minutes is usually a good balance for most organizations.

</p>
<p>
✅ And that’s it — you’ve successfully deployed an Account Lockout Policy through Group Policy in your Active Directory environment.
