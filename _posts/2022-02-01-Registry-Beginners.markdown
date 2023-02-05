---
layout: post
title: "A Sneak peek into Windows Registry Hives"
date: 01-04-2022 12:32:45 +0100
category: DFIR
---

# Registry Hives? What are they?

Windows registry in technical terms is a hierarchical database used to store user preferences, settings of installed programs, hardware devices and configuration of operating system. It can also be thought of DNA of the Windows Operating System.

![regedit](/assets/images/regedit.jpg#center)
Registry Editor
{: .image-caption}


## What is a Hive ? 
A hive is a logical group of subkeys, keys, and values in the registry that has a set of supporting files loaded into memory when the operating system starts or a user logs in.

The main five hives in Windows in Windows Registry are as follows:-
<ol>
  <li>HKEY_CLASSES_ROOT</li>
  <li>HKEY_CURRENT_USER</li>
  <li>THKEY_LOCAL_MACHINE</li>
  <li>HKEY_USERS</li>
  <li>HKEY_CURRENT_CONFIG
  </li>
</ol> 


## 1. HKEY_CLASSES_ROOT
<br />

![HKCR Hive](/assets/images/hkroot.jpg#center)
HKCR Hive
{: .image-caption}

The above screenshot is of the hive, HKEY_CLASSES_ROOT, which is a collection of file extensions as well as as well as a programmatic identifier (ProgID), Class ID (CLSID), and Interface ID (IID) data.

---

## 2. HKEY_CURRENT_USER
<br />

![HKCU Hive](/assets/images/hkcu.jpg#center)
HKCU Hive
{: .image-caption}

The above screenshot is of the hive, HKEY_CURRENT_USER, which stores the windows and software configurations specific to the logged in user. There are multiple user level settings related to the printers, desktop wallpaper, display settings, environment variables, keyboard layout, recently opened files and much more. 

This hive is stored in the NTUSER.dat. Most of the forensic artifacts are located in the NTUSER.dat\Software\Microsoft\Windows.

![Firefox Launcher](/assets/images/firefox.jpg#center)
Firefox Launcher
{: .image-caption}

In the screenshot above, we can see the path of the Firefox Launcher that we launched.  

---

## 3. HKEY_LOCAL_MACHINE
<br />

![HKLM Hive](/assets/images/hklm.jpg#center)
HKLM Hive
{: .image-caption}

HKLM (HKEY_LOCAL_MACHINE) and HKCU (HKEY_CURRENT_USER) are similar. HKLM holds information about the computer as a whole whereas HKCU holds information only about the current user and about the users who have logged in at but have since “switched users”. If a user is changing the HKCU keys, the changes would be reflected only on the user. Whereas, if the user is changing HKLM keys, it would be for every user using the machine.  


HKLM consists of following keys:-
<ol>
  <li>SAM</li>
  <li>SYSTEM</li>
  <li>SECURITY</li>
  <li>HARDWARE</li>
</ol> 

###### SAM

SAM (Security Accounts Manager) is a database registry file containing username and passwords. The file is like a locked diary with username/passwords. It can’t be accessed by any user as it is encrypted. The Windows local account credentials while logging in is checked against the hash in the SAM database file.

The SAM registry file is located on your system at C:\WINDOWS\system32\config. It is difficult to get hold of this file as most of the authentication happens through the domain controller in the Active Directory. In an enterprise scenario, compromising AD (Active Directory) would be the first priority.

---

## 4. HKEY_USERS
<br />

![HKU Hive](/assets/images/hku.jpg#center)
HKU Hive
{: .image-caption}

Each registry key under the HKEY_USERS hive corresponds to a user on the system and is names with that user’s security identifier, or SID. Inside the keys, Console, Printers, Keyboard, Desktop wallpaper and layout, Disk configuration of each of the users are present.


In the above example the built-in system accounts are .DEFAULT, S-1–5–18, S-1–5–19, S-1–5–20. “Real user accounts” are the ones with S-1–5–21-xxxxx. In this case, there is only one real account which the one ending in 500.

---

## 5. HKEY_CURRENT_CONFIG 
<br />


![HKCC Hive](/assets/images/hkcc.jpg#center)
HKCC Hive
{: .image-caption}

HKEY_CURRENT_CONFIG hive is a shortcut or a pointer directly to the hardware profile currently used which is in the hive, HKEY_LOCAL_MACHINE’s key, HKLM->SYSTEM->Current_Control_Set->Hardware Profiles->Current. This registry hive only exists for convenience. HKCC consists of Software and System from the HKLM’s Current key.