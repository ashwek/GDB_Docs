# 25 GDB Text User Interface

----

The GDB Text User Interface (TUI) is a terminal interface which uses the ``curses`` library to show the source file, the assembly output, the program registers and GDB commands in separate text windows. The TUI mode is supported only on platforms where a suitable version of the curses library is available.

The TUI mode is enabled by default when you invoke GDB as ``gdb -tui``.


----

## 25.1 TUI Overview

In TUI mode, GDB can display several text windows:
```
command
```
This window is the GDB _command_ window with the GDB prompt and the GDB output. The GDB input is still managed using readline.

```
source
```
The source window shows the source file of the program. The current line and active breakpoints are displayed in this window.

```
assembly
```
The assembly window shows the disassembly output of the program.

```
register
```
This window shows the processor registers. Registers are highlighted when their values change.

The source and assembly windows show the current program position by highlighting the current line and marking it with a ‘>’ marker.

The source, assembly and register windows are updated when the current thread changes, when the frame changes, or when the program counter changes.

These windows are not all visible at the same time. The command window is always visible. The others can be arranged in several layouts:
 - source only,
 - assembly only,
 - source and assembly,
 - source and registers, or
 - assembly and registers.

These are the standard layouts, but other layouts can be defined.

----

## 25.2 TUI Key Bindings

The TUI installs several key bindings in the readline keymaps. The following key bindings are installed for both TUI mode and the GDB standard mode.

``Ctrl + x`` ``A``

Enter or leave the TUI mode. When leaving the TUI mode.

``Ctrl + x`` ``1``

Use a TUI layout with only one window. The layout will either be ‘source’ or ‘assembly’. When the TUI mode is not active, it will switch to the TUI mode.

``Ctrl + x`` ``2``

Use a TUI layout with at least two windows. When the current layout already has two windows, the next layout with two windows is used.

``Ctrl + x`` ``o``

Change the active window. The TUI associates several key bindings with the active window. This command gives the focus to the next TUI window.

``Ctrl + x`` ``s``

Switch in and out of the TUI SingleKey mode that binds single keys to GDB commands.

----

## 25.4 TUI-specific Commands

The TUI has specific commands to control the text windows. These commands are always available, even when GDB is not in the TUI mode.

```
tui enable | disable
```
Activate / Disable TUI mode.

```
info win
```
List and give the size of all displayed windows.

```
tui new-layout name window weight [window weight…]
```
Create a new TUI layout. The new layout will be named _name_, and can be accessed using the ``layout`` command.

Each window parameter is either the name of a window to display, or a window description. The windows will be displayed from top to bottom in the order listed.

The names of the windows are the same as the ones given to the focus command; additional, the status window can be specified. Note that, because it is of fixed height, the weight assigned to the status window is of no importance. It is conventional to use ‘0’ here.

A window description looks a bit like an invocation of ``tui new-layout``, and is of the form ``{[-horizontal]window weight [window weight…]}``.

Each weight is an integer. It is the weight of this window relative to all the other windows in the layout. These numbers are used to calculate how much of the screen is given to each window.

For example:
```
(gdb) tui new-layout example src 1 regs 1 status 0 cmd 1
```
Here, the new layout is called ‘example’. It shows the source and register windows, followed by the status window, and then finally the command window. The non-status windows all have the same weight, so the terminal will be split into three roughly equal sections.

Here is a more complex example, showing a horizontal layout:
```
(gdb) tui new-layout example {-horizontal src 1 asm 1} 2 status 0 cmd 1
```
This will result in side-by-side source and assembly windows; with the status and command window being beneath these, filling the entire width of the terminal. Because they have weight 2, the source and assembly windows will be twice the height of the command window.

```
layout [next | prev | src | asm | split | regs | user_defined]
```
Changes which TUI windows are displayed. The parameter controls which layout is shown. It can be either one of the built-in layout names, or the name of a layout defined by the user using tui new-layout.

```
focus [next | prev | src | asm | regs | cmd]
```
Changes which TUI window is currently active for scrolling.

```
winheight name +count
winheight name -count
```
Change the height of the window name by count lines. Positive counts increase the height, while negative counts decrease it. The name parameter can be one of src (the source window), cmd (the command window), asm (the disassembly window), or regs (the register display window).

----

## 25.5 TUI Configuration Variables

Several configuration variables control the appearance of TUI windows.

```
set tui border-kind [space | ascii | acs]
```
Select the border appearance for the source, assembly and register windows.

```
set tui border-mode [normal | standout | reverse | half | half-standout | bold | bold-standout]
set tui active-border-mode [normal | standout | reverse | half | half-standout | bold | bold-standout]
```
Select the display attributes for the borders of the inactive windows or the active window.

```
set tui tab-width nchars
```
Set the width of _tab_ stops to be nchars characters. This setting affects the display of TAB characters in the source and assembly windows.
