# How to generate public key to access Secure FTP

## Generate SSH keys

 You can set up your server to authenticate users using the service managed authentication method, where user names and SSH keys are stored within the service. The user's public SSH key is uploaded to the server as a user's property. This key is used by the server as part of a standard key-based authentication process. Each user can have multiple public SSH keys on file with an individual server. For limits on number of keys that can be stored per user, see the [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the _AWS General Reference_.

 As an alternative to the service managed authentication method, you can authenticate users using a custom identity provider. This allows you to plug in an existing identity provider using an Amazon API Gateway endpoint. For more information, see [Authenticate using custom identity providers](https://docs.aws.amazon.com/transfer/latest/userguide/authenticating-users.html#authentication-custom-ip).

A server can only authenticate users using one method \(service managed or custom identity provider\), and that method cannot be changed after the server is created.

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



