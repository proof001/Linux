https://community.kde.org/KWin/Debugging
# Getting diagnosis information for bug reports

If you want to fetch relevant information to report a bug with KWin, the following command will provide a general list of data that should help the KWin developers diagnose your problem.

qdbus org.kde.KWin /KWin supportInformation

Depending on your distro (e.g. openSUSE), by default the command might be named a bit differently:

qdbus-qt5 org.kde.KWin /KWin supportInformation

On occasion, `xwininfo` might be asked for by the developers if the issue concerns screens and windows, and `xprop` if the issue concerns window information. After running either of those two commands, you'll need to click the window that's showing issues.

  

# Report issues via DrKonqi

Generally speaking, Plasmashell handles all widgets (including the menu), KWin handles windows and compositing (such as window decorations and desktop effects), and KGlobalAccel5 handles keyboard shortcuts.

In a situation where the Plasmashell and KGlobalAccel5 processes are still running but KWin (X11) has crashed, you will probably see a sad face in your notification tray, that's DrKonqi, the KDE Crash Handler, getting sad that you experienced a crash. Click its icon and you should be able to follow through with the crash reporting process in a straightforward manner.

In a situation where KGlobalAccel5 is still running but both Plasmashell and KWin have crashed, you can still invoke any keyboard shortcut to run a program that allows you to run a command, such as KRunner, Konsole or Yakuake. With that, you can restart the plasmashell process with:

plasmashell --replace

Or if you have manually enabled the new systemd initialization:

systemctl --user restart plasma-plasmashell

And you'll get a DrKonqi icon on your panel mentioning the KWin crash.

In case you were unable to create a backtrace using the KDE Crash Handler or you are using the Wayland session, proceed to the section [Debug KWin with GDB](https://community.kde.org/KWin/Debugging#Debug_KWin_with_GDB).

## Install debug symbols

Depending on your distribution, you might need additional steps before you're able to install debug symbols, as detailed on the [instructions on how to install debugging packages](https://community.kde.org/Guidelines_and_HOWTOs/Debugging/How_to_create_useful_crash_reports#Install_debugging_packages "Guidelines and HOWTOs/Debugging/How to create useful crash reports").

# Debug KWin with GDB

## TL;DR for bug reporters

For ease of reference, users wanting to report a KWin crash can just copy-paste the following two commands, wait for the crash to happen and ignore the rest of this page. You'll get a file named kwin.gdb in your home folder (or wherever folder you run this command).

For KWin on the X11 session:

echo 0 | sudo tee /proc/sys/kernel/yama/ptrace_scope
gdb -pid $(pidof kwin_x11) -batch -ex "set logging file kwin_x11.gdb" -ex "set logging on" -ex "continue" -ex "thread apply all backtrace" -ex "quit"

For KWin on the Wayland session:

echo 0 | sudo tee /proc/sys/kernel/yama/ptrace_scope
sudo gdb -pid $(pidof kwin_wayland) -batch -ex "set logging file kwin_wayland.gdb" -ex "set logging on" -ex "continue" -ex "thread apply all backtrace" -ex "quit"

![](https://community.kde.org/images.community/c/c1/Note-box-icon.png)

**Note**

If you get a message stating "tee: /proc/sys/kernel/yama/ptrace_scope: No such file or directory", that means your distribution kernel does not have yama enabled, that is, this security module won't hinder you from attaching GDB to KWin. You can safely ignore this error.

  
If you want to know what these commands do (recommended), keep reading.

## General information

While interacting with GDB, the debugged process is stopped - that's of course nasty if the debugged process is what paints what you see and handles your input.

KWin used to have issues with attaching GDB, but it is no longer the case on X11. Nevertheless, if you ever encounter issues doing this, you'll need to debug KWin from a side-channel, eg. **another TTY** or **via SSH** depending on what's available on your system. On Wayland, logging in via SSH is mandatory for interactive debugging because KWin is responsible for input handling and VT switching.

![](https://community.kde.org/images.community/c/c1/Note-box-icon.png)

**Note**

Debugging from an SSH connection is generally preferable over a TTY, since it doesn't impact the framebuffer/scanout buffer state.

  

## GDB says "ptrace: Operation not permitted."

This is probably the first thing you'll need to circumvent. By default, you're not allowed to attach GDB to KWin on a kernel which has the **Yama** security module enabled.

**Yama** is a kernel security feature which might or might not be enabled depending on your distro. In case it is, you'll need to explicitly allow GDB to attach to a non-inferior process:

echo 0 | sudo tee /proc/sys/kernel/yama/ptrace_scope

## Do I have to write down the debug output by hand ????

No ;-)

You just copy the gdb output into a file.

gdb --pid `pidof kwin_x11` 2>&1 | tee kwin.gdb

Alternatively, you can use the lengthier method made available by GDB.

gdb --pid `pidof kwin_x11`
set logging file kwin.gdb
set logging on

## I know nothing about GDB, how do I obtain a stacktrace?

A stacktrace (or backtrace) is a set of data containing information of the state the program was when it crashed. It is the primary means for the KWin developers to find out what happened on your machine.

Nowadays it's common for programs to take advantage of multiple threads to run more efficiently and make better use of the CPU cores available on your machine. Different threads might run different parts of a program, and each thread can render a different stacktrace.

So after attaching GDB to the application process, you'll see the GDB shell. It's where you'll run instructions so GDB can fetch the information you want.

Immediately after attaching GDB, it will stop the process, but you'll likely want to cause a certain condition (halt or crash) while KWin is running - in that case you first need to

continue

the process before it can be crashed.

If KWin does not crash, but you want to inspect the stack at some other time, you'll first need to interrupt the process by pressing

**Ctrl+C**

To dump a stacktrace, issue

bt

With this command you will get the stacktrace for the main thread where KWin crashed.

Then, hit the

**Enter**

key until you reach the end of the stack.

Sometimes, you may want to see what's in another thread

thread 2
bt
thread 3
bt

Alternatively, to dump a stacktrace the same way DrKonqi does (i.e. showing all available threads), use

thread apply all backtrace

This is probably the best method if you want to provide some awesome stacktraces for the KWin devs!

Finally, to leave GDB:

detach
quit

## Automating the creation of backtraces

GDB provides an easy way to automate debugging: the `-batch` flag. After enabling it, you should be able to run commands sequentially with `-ex` or `--eval-command`. A more detailed explanation of the procedure can be seen in [Plasma/Debugging](https://community.kde.org/Plasma/Debugging "Plasma/Debugging").

gdb -pid $(pidof kwin_x11) -batch -ex "set logging file kwin.gdb" -ex "set logging on" -ex "continue" -ex "thread apply all backtrace" -ex "quit"

## Function call traces

Here is GDB script allowing you to get function call traces without pausing KWin process, so you don't end up with halted session while the debugging:

$ cat ~/kde/gdb-x
set pagination off

break KGlobalAccelImpl::x11KeyPress(xcb_key_press_event_t*) 
break TabBox::keyPress(int )
break /home/bam/kde/src/kde/workspace/kwin/src/tabbox/tabbox.cpp:555

commands 1-20
# FIXME: for some reason KWin halts on any stepping command here, ideas?
#next
continue
end

continue &

Run the script as follows:

sudo gdb attach $(pidof kwin_wayland) -x ~/kde/gdb-x

It would be nice to adopt it for stepping commands also, ideas are welcome.

# Debug KWin with Valgrind

[It is not possible to attach Valgrind to running processes for fetching backtraces](https://www.valgrind.org/docs/manual/faq.html#faq.attach%7C), but it is possible for Valgrind to run a nested KWin Wayland session with an XWayland server running rootless:

dbus-run-session valgrind --log-file=kwinxwayland.log kwin_wayland --xwayland

And a pure KWin Wayland session:

dbus-run-session valgrind --log-file=kwinwayland.log kwin_wayland

KWin X11 is limited to using the currently running dbus session, and therefore it cannot produce nested sessions. The --replace flag is used for substituting your current kwin_x11 process.

valgrind --log-file=kwinx11.log kwin_x11 --replace

![](https://community.kde.org/images.community/c/c1/Note-box-icon.png)

**Note**

It's not possible to run a KWin X11 session from a KWin Wayland session.

In addition to creating backtraces, Valgrind is also able to log memory leaks.

valgrind --leak-check=full --show-reachable=yes --track-origins=yes --trace-children=yes --log-file=kwinxwaylandmem.log dbus-run-session kwin_wayland --xwayland"

# Automatically fetch core dumps with coredumpctl

After installing systemd-coredumpctl, you should now have a file located in /etc/systemd/coredump.conf that can be used to configure coredumpctl.

The Storage= setting defaults to external. This means that core dumps, in addition to being available through coredumpctl, are stored as physical files under /var/lib/systemd/coredump/. If you wish to be able to rotate core dumps together with the journal, you might want to set Storage=journal.

![](https://community.kde.org/images.community/c/cb/Warning.png)

**Warning**

Older versions off kwin_wayland have a non-dumpable process, which means coredumpctl is unable to fetch a full backtrace, rendering only truncated core dumps. In that case, those are still useful, but if possible, SSH into your session and attach GDB directly. See https://invent.kde.org/plasma/kwin/-/issues/33

  

![](https://community.kde.org/images.community/c/c1/Note-box-icon.png)

**Note**

Older versions of kwin_wayland used to throw the user back to the login screen if it it got killed (SIGKILL) or suffered a segmentation fault (SIGSEGV). As per https://invent.kde.org/plasma/kwin/-/merge_requests/483, SIGSEGV no longer causes this issue.

  
The main instructions on using coredumpctl to fetch are available on [the wiki page on crash reporting](https://community.kde.org/Guidelines_and_HOWTOs/Debugging/How_to_create_useful_crash_reports#Retrieving_a_backtrace_using_coredumpctl "Guidelines and HOWTOs/Debugging/How to create useful crash reports"). Basically, it amounts to this:

coredumpctl → check the PID of the crashed process → coredumpctl dbg <KWin PID here> → bt → copy into a log file

Or, alternatively:

coredumpctl dump <KWin PID>

It's possible to create a log file containing the backtrace by setting the --output flag to cat and redirecting it to a file:

coredumpctl dump <KWin PID> --output=cat > kwincrash.log

# Getting debug log output

The environment variable QT_LOGGING_RULES can be used to turn on full debug output from KWin:

export QT_LOGGING_RULES="kwin_*.debug=true"

You can append the environment variable to your ~/.bash_profile or to /etc/environment. If you are a bug tester, you might prefer to use /etc/environment since it's a common workflow to create new users for bug testing.

The logs for X11 are located in:

~/.xsession-errors

The logs for Wayland are located in:

~/.local/share/sddm/wayland-session.log

## What if KWin crashes upon login in a Wayland session?

You can still get additional information about the crash by logging in via a TTY (Ctrl + Alt + F3 for example) and running

export QT_LOGGING_RULES="kwin_*.debug=true"
startplasma-wayland > ~/startplasma-wayland.log 2>&1

By default, if KWin crashes multiple times in a row, it stops attempting to run, so just wait until it does.

After that, you may switch to the TTY where SDDM is running (usually either Ctrl + Alt + F1 or F7), login through the X11 session and report the issue.