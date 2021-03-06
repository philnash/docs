<!--
title: 16 - Using two-factor authentication
featured: true
-->

# Using Two-Factor Authentication

To meet the increasing need for strong digital security, npm has introduced two-factor authentication (2FA) to profiles and tokens. 2FA prevents unauthorized access to your accounts and projects. You have probably used 2FA before. For example, if you need to provide a code from your phone in addition to logging in with a password to access your bank account, your bank has enabled 2FA. Two-factor means that there are two pathways you must use to gain access to code or an account. 2FA would also include having a card key to get into a building, plus a physical key to get into an office. If you had one without the other, you could not get into the office.

To get started using 2FA with npm you will need to have an authentication package that can provide the second authentication factor. If you don't have one, please download a product such as [Authy](https://authy.com/download/) or [Google Authenticator](https://support.google.com/accounts/answer/1066447). 

(Note: npm will not use SMS (text-to-phone) as a method for authenticating users.)

## Summary of Features

As part of the introduction of 2FA, npm has enhanced or added new security features. Read this doc to learn how to use them.

### New Security Options

* Enable two-factor authentication on your user profile to prevent spoofing
* Profiles can be edited from the command line interface
* You can change passwords from the command line interface
* You can edit profile settings from the command line, including passwords
* Limit access to your code according to IP address ranges (CIDR)
* One-time use Password Recovery codes have been implemented for greater security
* Limit code to read or read-write control by controlling tokens
* Create and delete specialized tokens to allow targeted and controlled distribution

### Understanding Access Settings

For several of the new commands, you can select between two levels of authentication:

*   *auth only* means authenticate only, which gives you read access.
*   *auth-and-writes* means read, write, and delete access. Someone with this access can also grant access to others.

## Working with the new Profile Options

### Quick Start: New Profile Commands

  `npm profile enable-tfa [auth-only|auth-and-writes]`

  `npm profile disable-tfa`

  `npm profile get`

  `npm profile set [email|two factor auth|cidr_whitelist|fullname|homepage|freenode|twitter|github]`

## How to Add Two-Factor Authentication to your Profile

The first step toward greater security is to add 2FA to your profile. This will prevent spoof attacks, where someone logs in as if they were you.

1.  Enter the command to enable two factor authentication

    1.  Type either of these commands to enable tfa authentication and enable write access to your profile:

        ````
        npm profile enable-tfa
        npm profile enable-tfa auth-and-writes
        ````

    2.  Type this command to enable tfa authentication-only to your profile:

        ````
        npm profile enable-tfa auth-only
        ````

2.  Check you have chosen the right setting.

    1.  If you choose the default setting, this message will appear:

        ````
        $ npm profile enable-tfa

        > npm notice profile Enabling two factor authentication for auth-and-writes
        ````

    2.  If you chose the `auth-and-writes` tfa setting, the same message will appear:
        ````
        $ npm profile enable-tfa auth-and-writes

        > npm notice profile Enabling two factor authentication for auth-and-writes
        ````

    3.  If you chose the `auth-only` tfa setting, this message will appear:

        ````
        $ npm profile enable-tfa auth-only

        > npm notice profile Enabling two factor authentication for auth-only
        ````

3.  When prompted, enter your npm password.

4.  npm will present a QVR code with this message:

    ````
    Scan into your authenticator app or enter code [**your code**]
    And an OTP code from your authenticator:
    ````

5.  Use your authenticator app to scan the code, or to enter the codes as directed. After you do this, you will see this message:

    ````
    TFA successfully enabled. Below are your recovery codes, please print these out.
    You will need these to recover access to your account if you lose your authentication device.
    ````

6.  This statement is followed by a series of codes. Please print them or save them as described in the message.

    >**WARNING**: You must save these codes somewhere safe, such as a location that is not normally near your device. If you lose the device that provides the second method of security, or forget your password, these codes will be your only way to get back online.

## How to Remove Two-Factor Authentication from your Profile

1.  To remove 2FA from your profile, type this command:

    ````
    npm profile disable-tfa
    ````

2.  Enter your npm password when prompted.

3.  Enter a one-time password from your authenticator. The authenticator can be Authy or any other standard authenticators. Your screen will look like this:

    ````
    $ npm profile disable-2fa

    > npm password:

    >Enter one-time password from your authenticator: 123456

    Two factor authentication disabled.
    ````

### Note

The commands `npm profile enable-tfa` and `npm profile enable-2fa`, with or without dash `'-'`, are aliases. Similarly, `npm profile disable-tfa` and `npm profile disable-2fa`, with or without dash `'-'` are aliases.