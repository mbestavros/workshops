# The Windows Subsystem for Linux
Traditionally, Windows has been viewed as an inferior operating system for developers due to its lack of crucial tools available on Linux or Linux-like systems such as MacOS. Windows equivalents either wouldn't exist or be woefully under-supported and sometimes feature-incomplete next to their Linux counterparts. So, what's a Windows user to do if they want to get hacking?

For years, the default answer was simply to install Linux... or get a Mac. Neither of which were good solutions! Like it or not, Linux can be a hassle, and it's not always the best experience for complete beginners. And a new (expensive) computer is just not feasible in most cases.

Enter the Windows Subsystem for Linux, often abbreviated as "WSL."

Put simply, WSL allows you to run full-blown Linux distributions inside Windows, as if they were just another app like your browser or text editor. This is a _fantastic_ ability, allowing people to start using Linux's rich dev tools with much less hassle than before. It's developed by Microsoft as an officially-supported part of Windows, and has only been around for a few years -- but in that time, it's proven to be the easiest way for Windows people to use Linux.

Today, we're going to run through how to set up and get started using it. This guide will mirror the [official guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) very closely -- just with additional instructions or clarifications where needed for complete beginners, and with some handy additional quality-of-life tips at the end.

## What you'll need
- A Windows computer running the Windows 10 Anniversary Update. If your Windows PC is reasonably up to date, you should have this -- though the more up-to-date, the better.
- An administrator account.
- An Internet connection (or [install media](https://docs.microsoft.com/en-us/windows/wsl/install-manual))

## Enabling WSL components
The Windows components needed to run WSL are not enabled by default, so we'll need to flip that switch first.

First, open an administrator `Powershell` terminal:
- Right-click your Windows button, find and click on "Powershell (Admin)", and click "Allow" on the Administrator prompt.

Then, copy and paste this line into the Powershell terminal, and hit Enter:

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

This should prompt you to restart your computer. Do so.

Once you're back up, you're ready to install WSL!

## Getting a Linux distro
There are multiple ways to go about getting a Linux distro. If you're running Windows build `16215` or later, you can use the Microsoft store to browse and install distros like any other app. Alternatively, you can install them [manually](https://docs.microsoft.com/en-us/windows/wsl/install-manual). I've included a section below with more details.

### Wait... what's a distro? Which ones should I use?
"Distro" is just shorthand for "distribution". Because Linux is open source, it's freely modifiable -- and the Linux community frequently releases new versions, each with slightly different features and focus. These versions are referred to as "distros". For example, Red Hat publishes a Linux distro called Fedora. Canonical publishes one called Ubuntu. The list goes on and on.

If you don't have any strong preference, I'd recommend Ubuntu to start. It's officially supported by both Canonical (its developer) and Microsoft, and will probably give you the least grief.

## Manually installing a Linux distro