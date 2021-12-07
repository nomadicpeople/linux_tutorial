# Visual Studio Code Remote Development Extension Pack

The Remote Development extension pack allows you to open any folder in a container, on a remote machine, or in the Windows Subsystem for Linux (WSL) and take advantage of VS Code's full feature set. Since this lets you set up a full-time development environment anywhere, you can:

1. Develop on the same operating system you deploy to or use larger, faster, or more specialized hardware than your local machine.
2. Quickly swap between different, separate development environments and make updates without worrying about impacting your local machine.
3. Help new team members / contributors get productive quickly with easily spun up, consistent development containers.
4. Take advantage of a Linux based tool-chain right from the comfort of Windows from a full-featured development tool.

## Installation



1.Install VS Code or VS Code Insiders and this extension pack. On Windows, be sure to check Add to PATH when asked to Select Additional Tasks during installation.

2.Remote - SSH: Install an OpenSSH compatible SSH client.

3.Remote - WSL: Install the Windows Subsystem for Linux along with your preferred Linux distribution. (Note that WSL2 support is experimental.)

4.Remote - Containers: Install and configure Docker for your operating system.
    - Windows / macOS:
    Install Docker Desktop 2.0+ for Mac/Windows. Windows 10 Home (2004+) requires Docker Desktop 2.2+ and the WSL2 back-end. (Docker Toolbox is not supported.) 
    To enable the Windows WSL2 back-end: Right-click on the Docker taskbar item and select Settings. Check Use the WSL2 based engine and verify your distribution is enabled under Resources > WSL Integration.
    - Linux:
    Follow the official install instructions for Docker CE/EE 18.06+. If you use Docker Compose, follow the Docker Compose 1.21+ install directions.
    Add your user to the docker group by using a terminal to run: sudo usermod -aG docker $USER Sign out and back in again so this setting takes effect.

## Getting Started

Available commands

Another way to learn what you can do with the Remote Development extensions is to browse the commands each of them provide. Press F1 to bring up the Command Palette and type in Remote- for a full list of commands.
For more information, please see the extension pack documentation.
