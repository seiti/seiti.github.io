---
layout: post
title: Para os que não vivem sem um terminal de linha de comando
date: '2006-12-07 19:42:27'
tags:
- shell
- windows
---


Comandos do Linux com correspondentes no Windows:

- **crontab**: <tt>at</tt> (XP/2000), <tt>schtasks</tt> (XP only)
- **chmod**: <tt>cacls</tt> (XP, 2000, & NT4.0)
- **diff**: <tt>comp</tt> (XP & 2000) mas não presta
- **vi**: <tt>edit</tt> tá bom, não é a mesma coisa
- **fdisk**: <tt>diskpart</tt> (XP only)
- **lsmod, lsusb, lspci**: <tt>driverquery</tt> (XP only), <tt>msinfo32</tt> (XP & 2000)
- **ifconfig**: <tt>getmac</tt> (XP & 2000), <tt>ipconfig</tt> (XP, 2000 & NT4.0), <tt>netsh</tt> (XP & 2000)
- **more** ou **less**: <tt>more</tt>
- **uptime**: <tt>net statistics server</tt>
- **tracert**: <tt>pathping</tt> (XP & 2000)
- **/etc/grub/**: <tt>bootcfg</tt> (XP only)
- **/etc/init.d/**: <tt>sc</tt> (XP & 2000)
- **procinfo**: <tt>systeminfo</tt> (XP only)
- **shutdown**, **halt**: <tt>shutdown</tt> (XP & 2000)
- **top**: <tt>tasklist</tt> (XP pro only)
- **kill**: <tt>taskkill</tt> (XP only)

E alguns comandos úteis do Windows:

- **contig** (works with NT4.0 and newer): A great defrag utility for NTFS partitions.
- **control** (XP only) – unpublished!: Allows you to launch control panel applets from the command line. <tt>control userpasswords2</tt>, for example will launch a helpful local user admin utility.
- **defrag** (XP only – NT4.0 and Windows 2000 use contig): Yes, XP comes with a command line disk defrag utility. If you are running Windows 2000 or NT4.0 there is still hope. Contig is a free defrag program that I describe on the defrag page.
- **eudcedit** (XP only): Private Character editor. Yes with this program built into Windows XP you can create your own font!
- **fsutil** (XP only): This is a utility with a lot of capability. Come back soon for great examples.
- **gpresult** (XP & 2000): This generates a summary of the user settings and computer group policy settings.
- **gpupdate** (XP only): Use this utility to manually apply computer and user policy from your windows 2000 (or newer) domain.
- **MMC** (XP, 2000 & NT4.0) – Microsoft Management Console. This is the master tool for Windows, it is the main interface in which all other tools use starting primarily in Windows 2000 and newer systems.
- **msconfig** (XP only): The ultimate tool to change the services and utilities that start when your Windows machine boots up. You can also copy the executable from XP and use it in Windows 2000.
- **narrator** (XP only): Turns on the system narrator (can also be found in accessibility options in control panel). Will will allow your computer to dictate text to you.
- **nslookup** (all): A DNS name resolution tool.
- **openfiles** (XP Only): Allows an administrator to display or disconnect open files in XP professional. Type “openfiles /?” for a list of possible parameters.
- **recover** (XP & 2000): This command can recover readable information from a damaged disk and is very easy to use.
- **reg** (XP & 2000): A console registry tool, great for scripting Registry edits.
- **secedit** (XP & 2000): Use this utility to manually apply computer and user policy from your windows 2000 (or newer) domain. Example to update the machine policy: secedit /refreshpolicy machine_policy /enforce. To view help on this, just type secedit. NOTE: In Windows XP SP1 and news, this command is superceded by: gpupdate /force
- **sfc** (XP & 2000): The system file checker scans important system files and replaces the ones you (or your applications) hacked beyond repair with the real, official Microsoft versions.
- **sigverif** (XP only): Microsoft has created driver signatures. A signed driver is Microsoft tested and approved. With the sigverif tool you can have all driver files analyzed to verify that they are digitally signed. Just type ‘sigverif’ at the command prompt.
- **sysedit** (XP/2000): System Configuration File Editor. An old tool that was very handy for the Windows 9X days. msconfig is what you want to use now.
- **tree** (XP & 2000): An amazing experience everyone should try! This command will provide a ‘family tree’ style display of the drive/folder you specify.
- **WMIC** (XP & 2000): Windows Management Instrumentation Command tool. This allows you to pull an amazing amount of low-level system information from a command line scripting interface.

E para enviar um email por linha de comando não deixe de testar o script [mailsend](http://www.muquit.com/muquit/software/mailsend/mailsend.html).

[Lista oficial](http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/ntcmds.mspx?mfr=true)


