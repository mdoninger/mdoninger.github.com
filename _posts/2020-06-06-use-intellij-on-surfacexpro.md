---
layout: post
title: "Use IntelliJ and other JetBrains IDEs on Surface X Pro"
date: 2020-06-06T12:00:00+02:00
published: true
---


# Introduction
With the Surface X Pro, there are now a number of ARM based tablets and notebooks available.
One precondition for applications running on those devices is to either have a specific  
build for the ARM64 architecture, or to use a 32-bit Win32 application, which will run in an  
emulation on ARM (with a lower performance).

Jetbrains does not provide 32-bit versions for Windows anymore for any of its applications,  
so running them natively on Windows on ARM is not possible. There is however a workaround,  
which i want to document in this blog post.
I will use IntelliJ in the further examples, but the instructions apply to all other Jetbrains IDEs as well.

# WSL 2
As you might already know, Microsoft provides a performant virtualization technology for Linux  
distributions, which was just recently (in May) released in its second version. WSL 2 distributions  
can be downloaded through the Microsoft Store.  
WSL 2 works on the Surface X Pro, so you can run Linux distributions, that provide a build for ARM64.  
In this example, i will use Pengwin, but other distributions like Ubuntu or Debian are available as well.
As a precondition, you need to setup the WSL 2 distribution for GUI apps, which will include the installation
and configuration of an X Server on Windows (this is not covered in this post).

# Java runtime for Linux ARM64
There are different possibilities to get a JRE/JDK for Linux. You can either install it directly  
through the package manager of the distribution, or you can download the [Jetbrains Runtime](https://bintray.com/jetbrains/intellij-jbr/jbrsdk11-linux-aarch64/_latestVersion), which  
is also available for ARM64.

# Download the Jetbrains tools
You cannot use the Jetbrains Toolbox, since it's only provided for x86 and x64 architectures on Linux, but not ARM.
Thus you need to download each tool individually. If provided, choose a download without JBR (you can choose those versions
by clicking the link "Other versions" on the download pages of the individual tools).
After you have extracted the contents, go into the tool folder (e.g. idea-IU-201.7223.91), and check if there is a folder named
"jbr". You can safely delete this folder, since this version of the Jetbrains Runtime is either x86 or x64.
If you use a JRE provided by the package manager, you are good to go, otherwise if you want to use a custom
JRE to execute IntelliJ, copy this JRE into the IntelliJ folder with the folder name `jbr-x86`.

## fsnotifier
The IDEs have a native executable in their bin folder, called fsnotifier. This is not compiled for ARM, so it doesn't work.
Jetbrains has provided a [small documentation](https://confluence.jetbrains.com/display/IDEADEV/Compiling+File+Watcher). on how to compile it for ARM

# Add a shortcut in the Windows start menu
You can easily add a shortcut to your IntelliJ installation in the WSL 2 machine.
Open the folder `C:\Users\{YourUsername}}\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\`.
You can either create a subfolder there, or just the shortcut in that folder.
When creating the shortcut, add the following string as target:
`C:\Windows\System32\wscript.exe C:\\Users\\{yourUserName}\wslu\runHidden.vbs "pengwin.exe" run "cd ~; bash -l -c /home/{{username}}/path/to/intellij/bin/idea.sh"`

Create the following script with the path `C:\Users\{yourUserName}\wslu\runHidden.vbs` (you can also change a different path, but need to adapt
this path in the shortcut as well), and add the following content:

{% highlight vbs %}
' Mehthod by @mklement0 on Stack Overflow
' https://stackoverflow.com/questions/41225711/wsl-run-linux-from-windows-without-spawning-a-cmd-window
' Usage: wscript .\runHidden.vbs bash -c <COMMAND>
' Simple command-line help.
select case WScript.Arguments(0)
case "-?", "/?", "-h", "--help"
  WScript.echo "Usage: runHidden executable [...]" & vbNewLine & vbNewLine & "Runs the specified command hidden (without a visible window)."
  WScript.Quit(0)
end select

' Separate the arguments into the executable name
' and a single string containing all arguments.
exe = WScript.Arguments(0)
sep = ""
for i = 1 to WScript.Arguments.Count -1
  ' Enclose arguments in "..." to preserve their original partitioning.
  args = args & sep & """" & WScript.Arguments(i) & """"
  sep = " "
next

' Execute the command with its window *hidden* (0)
WScript.CreateObject("Shell.Application").ShellExecute exe, args, "", "open", 0
{% endhighlight %}