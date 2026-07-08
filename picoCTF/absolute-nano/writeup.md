# writeup

![picoCTF](https://img.shields.io/badge/platform-picoCTF-orange?style=for-the-badge) ![Binary Exploitation](https://img.shields.io/badge/category-binary%20exploitation-red?style=for-the-badge) ![Status](https://img.shields.io/badge/status-solved-brightgreen?style=for-the-badge)

## Writeup - Absolute Nano (picoCTF)

***

### Challenge Information

* Category: Binary Exploitation / Privilege Escalation.
* Difficulty: Easy.
* Platform: picoCTF.

***

### Initial Access

The challenge starts with SSH access to a restricted user account.

![SSH Login](assets/1-ssh-login.png)

***

### Attempting to Read the Flag

Direct access to the flag file was denied because the user did not have enough permissions.

![Permission Denied](assets/2-cat-flag-denied.png)

***

### Failed Attempt

An early privilege escalation attempt modified `/etc/sudoers` incorrectly and broke `sudo` with a syntax error.

![Broken sudoers](assets/3-tried-copyfail-cve2026-31431-denied.png)

***

### Enumerating sudo Privileges

Running `sudo -l` showed that the user could execute `nano` as root without a password.

```bash
sudo -l
sudo /bin/nano /etc/sudoers
```

This suggested a shell escape through nano.
![Vulnerability Detected](assets/4-vulnerability-detected.png)

***

### Exploiting Nano

With `nano` running as root, the shell escape was triggered using:

* `Ctrl + R`
* `Ctrl + X`

This opened a root shell successfully.

![Run Command on sudoers](assets/5-run-command-on-sudoers.png)

### Gaining Root Access

After escaping from nano, root access was obtained and the flag became available.

![Root Access and Flag](assets/6-gained-access-root-n-discovered-flag.png)

***

### Flag

```
picoCTF{n4n0_411_7h3_w4y_d74f446b}
```

***

### Flag Submission

The recovered flag was submitted successfully on picoCTF.

![Flag Accepted](assets/7-flag-accepted.png)

***

### Lessons Learned

* Misconfigured `sudo` permissions can lead to full system compromise.
* Root-capable text editors may provide shell escapes.
* `sudo -l` is often enough to reveal the attack path.
* Incorrect edits to `/etc/sudoers` can break `sudo` completely.
* GTFOBins is very useful for privilege escalation paths.
