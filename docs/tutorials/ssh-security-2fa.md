# SSH Security - 2FA

Two-factor authentication involves requiring a second security measure in addition to your password or SSH key, usually on a separate device from your primary one.

For example, you may be familiar with logging into a website such as a crypto exchange using both a password and a Google Authenticator code (or an SMS code). This two-step process is an example of two-factor authentication.

SSH can also be configured to require a Google Authenticator code, which means that an attacker that somehow compromised your SSH key and its passphrase would **still need the device with the authenticator app on it** (presumably your phone). This adds an extra layer of security to your system.

!!! warning "Warning"
    It is **strongly recommended** that you open a second terminal with an SSH connection to your node, just in case you misconfigure something. This way, you will have a backup that is still connected in case you lock yourself out, so you can easily undo your mistakes.

    If you **do** manage to lock yourself out, you will need to physically access your node via its local monitor and keyboard to log in and repair the misconfiguration.


Start by installing [Google Authenticator (opens new window)](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2\&hl=en\_US\&gl=US)(or a compatible equivalent) on your phone if you don't already have it. For Android users, consider [andOTP (opens new window)](https://play.google.com/store/apps/details?id=org.shadowice.flocke.andotp\&hl=en\_US\&gl=US)which is an open-source alternative that supports password locking and convenient backups.

Next, install the Google Authenticator module on your node with this command:

```
sudo apt install -y libpam-google-authenticator
```

Now tell the `PAM` (pluggable authentication modules) to use this module. First, open the config file:

```
sudo nano /etc/pam.d/sshd
```

Find `@include common-auth` (it should be at the top) and comment it out by adding a `#` in front of it, so it looks like this:

```
# Standard Un*x authentication.
#@include common-auth
```

Next, add these lines to the top of the file:

```
# Enable Google Authenticator
auth required pam_google_authenticator.so
```

Then save and exit the file with `Ctrl+O`, `Enter`, and `Ctrl+X`.

Now that `PAM` knows to use Google Authenticator, the next step is to tell `sshd` to use `PAM`. Open the `sshd` config file:

```
sudo nano /etc/ssh/sshd_config
```

Now change the line `KbdInteractiveAuthentication no` to `KbdInteractiveAuthentication yes` so it looks like this:

```
# Change to yes to enable challenge-response passwords (beware issues with
# some PAM modules and threads)
KbdInteractiveAuthentication yes
```

(Older versions of SSH call this option `ChallengeResponseAuthentication` instead of `KbdInteractiveAuthentication`.)

Add the following line to the bottom of the file, which indicates to `sshd` that it needs both an SSH key and the Google Authenticator code:

```
AuthenticationMethods publickey,keyboard-interactive
```

Every option added to `AuthenticationMethods` will be required when you log in. So you can choose e.g. 2FA and password, or a combination of all three methods.

* `publickey` (SSH key)
* `password publickey` (password)
* `keyboard-interactive` (2FA verification code)

Then save and exit the file with `Ctrl+O`, `Enter`, and `Ctrl+X`.

Now that `sshd` is set up, we need to create our 2FA codes. In your terminal, run:

```
google-authenticator
```

First, it will ask you about time-based tokens. Say `y` to this question:

```
Do you want authentication tokens to be time-based: y
```

You will now see a big QR code on your screen; scan it with your Google Authenticator app to add it. You will also see your secret and a few backup codes looking like this:

```
Your new secret key is: IRG2TALMR5U2LK5VQ5AQIG3HA4
Your verification code is 282436
Your emergency scratch codes are:
  29778030
  86888537
  50553659
  41403052
  82649596
```

!!! info "Info"

  Record the emergency scratch codes somewhere safe in case you need to log into the machine but don't have your 2FA app handy. Without the app, you will no longer be able to SSH into the machine!


Finally, it will ask you for some more parameters; the recommended defaults are as follows:

```
Do you want me to update your "/<username>/.google_authenticator" file: y
Do you want to disallow multiple uses of the same authentication token: y
By default... < long story about time skew > ... Do you want to do so: n
Do you want to enable rate-limiting: y
```

Once you're done, restart `sshd` so it grabs the new settings:

```
sudo systemctl restart sshd
```

When you try to SSH into your server with your SSH keys, you should now also be asked for a 2FA verification code, but not for a password.

****[**Source ↗**](https://docs.rocketpool.net/guides/node/securing-your-node.html#optional-enable-two-factor-authentication)****
