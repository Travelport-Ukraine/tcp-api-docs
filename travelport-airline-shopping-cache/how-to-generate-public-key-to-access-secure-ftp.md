# Generating SSH keys

### Creating SSH Keys on macOS, Linux, or UNIX

On the macOS, Linux, or UNIX operating systems, you use the `ssh-keygen` command to create an SSH public key and SSH private key also known as a key-pair.

**To create SSH keys on a macOS, Linux, or UNIX operating system**

1. On macOS, Linux, or UNIX operating systems, open a command terminal.
2.  At the prompt, enter the following command: 

{% hint style="info" %}
 `key_name` is the SSH key-pair file name.
{% endhint %}

The following shows an example of the `ssh-keygen` output.

3. Navigate to the `key_name`.pub file and open it.  

4.  Copy the text and paste it in **SSH public key**.

{% hint style="info" %}
  When you run the `ssh-keygen` command as shown preceding, it creates the public and private keys as files in the current directory.
{% endhint %}

### Creating SSH Keys on Microsoft Windows:

Windows uses a slightly different SSH key-pair format. The public key must be in the `PUB` format, and the private key must be in the `PPK` format. On Windows, you can use PuTTYgen to create an SSH key-pair in the appropriate formats. You can also use PuTTYgen to convert a private key generated using `ssh-keygen` to a .ppk file.

{% hint style="info" %}
If you present WinSCP with a private key file not in .ppk format, that client offers to convert the key into .ppk format for you.
{% endhint %}

For a tutorial on creating SSH keys using PuTTYgen on Windows, see the [SSH.com website](https://www.ssh.com/ssh/putty/windows/puttygen).

