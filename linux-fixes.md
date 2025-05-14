# 📑 **Contents**

- [🛠️ 2025-05-14 – Cannot Change Monitor in Display App from 2560x1440 to 1920x1080](#️-2025-05-14--cannot-change-monitor-in-display-app-from-2560x1440-to-1920x1080)
- [🛠️ 2025-05-11 – Black Screen with Pointer After Login (Linux Mint + DisplayLink)](#️-2025-05-11--black-screen-with-pointer-after-login-linux-mint--displaylink)
- [Template](#template)

---
# **2025-05-14 – Cannot change monitor in Display app from 2560x1440 to 1920x1080**

**Issue**  
I get a black screen when the monitor is on resolution 2560x1440 because of DisplayLink, I cannot change the display resolution of 1 monitor to 1920x1080.

**System Info**  
- **Distro**: Linux Mint 22.1  
- **Kernel**: 6.8.0-59-generic  
- **Desktop**: Cinnamon  

**Fix / Solution**
    
You can manually change the monitor resolution using the `xrandr` command:

1. List all connected display outputs:

    ```bash
    xrandr
    ```

    Look for your monitor's identifier (e.g., `DVI-I-1-1`). It may vary.

2. Change the resolution:

    ```bash
    xrandr --output DVI-I-1-1 --mode 1920x1080
    ```

    Replace `DVI-I-1-1` with the correct output name from step 1 if different.

**Result**
Screen changed to 1920x1080 resolution and screen worked after that

# 🛠️ **2025-05-11 – Black Screen with Pointer After Login (Linux Mint + DisplayLink)**

## **Issue**

After installing **DisplayLink version 6.1.1**, I encountered a **black screen with a mouse pointer** after logging into my desktop (Linux Mint 22.1, Cinnamon).  
The issue worsened after each reboot.

## **System Information**

- **Distro**: Linux Mint 22.1  
- **Kernel**: 6.8.0-59-generic  
- **Desktop**: Cinnamon  

## **Diagnosis**

To rule out system-wide issues, I created a **test user** to see if Cinnamon worked correctly under a clean user environment.

### 🔹 Create a Test User from TTY

1. Switch to a terminal with `Ctrl + Alt + F2`
2. Log in and run:

	    sudo adduser testuser

3. Add the user to common groups:

	      sudo usermod -aG sudo,adm,dialout,cdrom,floppy,audio,video,plugdev,netdev testuser

4. Restart the display manager:

	    sudo systemctl restart lightdm
	
  5. Log in as testuser.

✅ Result: Cinnamon started correctly.
➡️ Conclusion: The issue was limited to the main user’s configuration in the home directory.


### Fix: Reset Broken User Configuration



 1. Log in to a TTY as your main user (Ctrl + Alt + F2)
 2. Rename the configuration directories to back them up:

	    mv ~/.config ~/.config_broken
	    mv ~/.cache ~/.cache_broken
	    mv ~/.local ~/.local_broken
	    mv ~/.xsession ~/.xsession_broken 2>/dev/null

 3. Restart the display manager:
		
		sudo systemctl restart lightdm

🔁 Upon next login, Cinnamon recreated all desktop settings from scratch.
✅ Result

    

 - Screen and session returned to normal.
 - Desktop is functional again under the main user account.

📝 Notes

   

 - Be sure to remove all DisplayLink-related files beforehand.
 - If this doesn’t help, try:
	 - Restoring a Timeshift snapshot from before the DisplayLink installation.
	 - Or logging in as another user to verify the problem is user-specific.

# **Template**

## **YYYY-MM-DD – [Short Issue Title]**

**Issue**  
Describe the problem in 1–2 sentences.

**System Info**  
- **Distro**: Linux Mint [version]
- **Kernel**: [your kernel version]
- **Desktop**: [Cinnamon / MATE / XFCE / Other]

**Fix / Solution**

    # Terminal commands or steps you followed

**Result**
What happened after applying the fix?

**Notes**
Any useful tips, causes, related links, or future steps.
