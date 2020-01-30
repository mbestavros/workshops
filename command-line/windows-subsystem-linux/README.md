# The Windows Subsystem for Linux
Traditionally, Windows has been viewed as an inferior operating system for developers due to its lack of crucial tools available on Linux or Linux-like systems such as MacOS. Windows equivalents either wouldn't exist or be woefully under-supported and sometimes feature-incomplete next to their Linux counterparts. So, what's a Windows user to do if they want to get hacking?

For years, the default answer was simply to install Linux... or get a Mac. Neither of which were good solutions! Like it or not, Linux can be a hassle, and it's not always the best experience for complete beginners. And a new (expensive) computer is just not feasible in most cases.

Enter the **Windows Subsystem for Linux**, often abbreviated as **"WSL."**

Put simply, WSL allows you to run full-blown Linux distributions inside Windows, as if they were just another app like your browser or text editor. This is a _fantastic_ ability, allowing people to start using Linux's rich dev tools with little hassle. It's developed by Microsoft as an officially-supported part of Windows, and has only been around for a few years -- but in that time, it's proven to be the easiest way for Windows people to use Linux.

Today, we're going to run through how to set up and get started using it. This guide will mirror the [official guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) very closely -- just with additional instructions or clarifications where needed for complete beginners, and with some handy additional quality-of-life tips at the end.

As of 1-31-2019, this guide is written specifically for delivery at **TechTogether 2020**. It will be updated for general use eventually (though the guide is substantially complete regardless).

## What you'll need
- A Windows computer running the Windows 10 Anniversary Update. If your Windows PC is reasonably up to date, you should have this -- though the more up-to-date, the better. (I wouldn't try updating while at the hackathon, though.)
- An administrator account.
- An Internet connection (or [install media](https://docs.microsoft.com/en-us/windows/wsl/install-manual))

## Enabling WSL components
The Windows components needed to run WSL are not enabled by default, so we'll need to flip that switch first.

First, open an administrator `Powershell` terminal:
- Right-click your Windows button
- Find and click on "Powershell (Admin)"
- Click "Allow" on the Administrator prompt.

Then, copy and paste this line into the Powershell terminal, and hit Enter:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

This should prompt you to restart your computer. Do so.

Once you're back up, you're ready to install WSL!

## Getting a Linux distro (...at TechTogether)
There are multiple ways to go about getting a Linux distro. If you're running Windows build `16215` or later, the easiest is probably to use the Microsoft Store to browse and install distros like any other app.

### Wait... what's a distro? Which one should I use?
"Distro" is just shorthand for "distribution". Because Linux is open source, it's freely modifiable -- and the Linux community frequently releases new versions, each with slightly different features and focus. These versions are referred to as "distros". For example, Red Hat publishes a Linux distro called Fedora. Canonical publishes one called Ubuntu. The list goes on and on.

If you don't have any strong preference, I'd recommend Ubuntu to start. It's officially supported by both Canonical (its developer) and Microsoft, and will probably have good help resources available online.

### What are we waiting for? Let's go!
Well... not quite yet. Using the Microsoft Store requires a good Internet connection... which I'm not willing to rely on during a hackathon. _(I've been burned before.)_ Fortunately, it's possible to install WSL [manually](https://docs.microsoft.com/en-us/windows/wsl/install-manual) with installation media (and no Internet connection!). So, for TechTogether 2020, that's what we'll be doing -- I've put the Ubuntu WSL install image on flash drives and will be distributing those to attendees. Hopefully, this should allow the process to go fairly smoothly.

When you plug in your flash drive, copy the file called `CanonicalGroupLimited.Ubuntu18.04onWindows(...).appx` file to your local `Downloads` folder. (It should be the only file on the flash drive.) Once done, you're ready to go -- just make sure to eject your drive and pass it on to someone else that needs it. (Or back to the front if everyone is done with it. Thank you!)

### Manually installing a Linux distro
Once you've downloaded (or moved, as will be the case during TechTogether) the install image (the Ubuntu `.appx` file), you're ready to manually install WSL!

You'll need to open a `Powershell` prompt, just like during the first step -- right click on your Windows button, then click `Powershell`.

Then, you'll need to navigate to your Downloads folder. **include commands to cd in admin/non admin here**

Once you're in your Downloads folder **insert how people can tell**, you'll want to install the image using this command:

```powershell
Add-AppxPackage .\CanonicalGroupLimited.Ubuntu18.04onWindows_1804.2018.817.0_x64__79rhkp1fndgsc.appx
```

Copy and paste it into Powershell, then press Enter. Let it do its thing.

When complete, you should have a new app in your start menu called "Ubuntu". Hooray! You can close your Powershell window now.

## Setting up your Linux distro
Every WSL distro needs to run through first-time setup before we can use it regularly. We'll start this process by opening the distro in our Start menu (it should be "Ubuntu" if you installed at TechTogether). This will open a Terminal window, and it'll tell you it's installing. This process will take some time, so if you get to this point early, help out your peers if they're a few steps behind!

The terminal will 