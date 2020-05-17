# GDB - GNU Debugger

[Online Documentation](http://sourceware.org/gdb/current/onlinedocs/gdb/)

----

#### [CppCon 2015: Greg Law " Give me 15 minutes & I'll change your view of GDB" - Youtube](https://www.youtube.com/watch?v=PorfLSr3DDI)

----

The purpose of a debugger such as GDB is to allow you to see what is going on “inside” another program while it executes—or what another program was doing at the moment it crashed.

----

<ol type="1">
    <li><a href="./1_A_Sample_GDB_Session.md">A sample GDB Session</a></li>
    <li>
        <a href="./2_Getting_In_and_Out_of_GDB.md">Getting In and Out of GDB</a>
        <ol type="1">
            <li><a href="./2_1_Invoking_GDB.md">Invoking GDB</a></li>
            <li><a href="./2_2_Quitting_GDB.md">Quitting GDB</a></li>
            <li><a href="./2_3_Shell_Commands.md">Shell Commands</a></li>
            <li><a href="./2_4_Logging_Output.md">Logging Output</a></li>
        </ol>
    </li>
    <li>
        <a href="./3_GDB_Commands.md">GDB Commands</a>
        <ol type="1">
            <li><a href="./3_1_Command_Syntax.md">Command Syntax</a></li>
            <li><a href="./3_2_Command_Settings.md">Command Settings</a></li>
            <li><a href="./3_3_Command_Completion.md">Command completion</a></li>
            <li><a href="./3_4_Command_Options.md">Command Options</a></li>
            <li><a href="./3_5_Getting_Help.md">Getting Help</a></li>
        </ol>
    </li>
    <li>
        <a href="./4_Running_Programs_Under_GDB.md">Running Programs Under GDB</a>
        <ol type="1">
            <li><a href="./4_1_Compiling_for_Debugging.md">Compiling for Debugging</a></li>
            <li><a href="./4_2_Starting_Your_Program.md">Starting your Program</a></li>
            <li><a href="./4_3_Your_Programs_Arguments.md">Your Programs Arguemnts</a></li>
            <li><a href="./4_4_Your_Programs_Environment.md">Your Programs Environment</a></li>
            <li><a href="./4_5_Your_Programs_Working_Directory.md">Your Programs Working Directory</a></li>
            <li><a href="./4_6_Your_Programs_Input_And_Output.md">Your Programs Input & Output</a></li>
            <li><a href="./4_7_Debugging_an_Already_Running_Process.md">Debugging an Already Running Process</a></li>
            <li><a href="./4_8_Killing_the_Child_Process.md">Killing the Child Process</a></li>
            <li><a href="./4_9_Debugging_Multiple_Inferiors_and_Programs.md">Debugging Multiple Inferiors & Programs</a></li>
            <li>Debugging programs with multiple threads</li>
            <li>Debugging forks</li>
            <li><a href="./4_12_Setting_a_Bookmark_to_Return_to_Later.md">Setting a Bookmark to Return to Later</a></li>
        </ol>
    </li>
    <li>
        <a href="./5_Stopping_and_Continuing.md">Stopping and Continuing</a>
        <ol type="1">
            <li>
                <a href="./5_1_Breakpoints_Watchpoints_Catchpoints.md">Breakpoints, Watchpoints, and Catchpoints</a>
                <ol type="1">
                    <li><a href="./5_1_1_Setting_Breakpoints.md">Setting Breakpoints</a></li>
                    <li><a href="./5_1_2_Setting_Watchpoints.md">Setting Watchpoints</a></li>
                    <li><a href="./5_1_3_Setting_Catchpoints.md">Setting Catchpoints</a></li>
                    <li><a href="./5_1_4_Deleting_Breakpoints.md">Deleting Breakpoints</a></li>
                    <li><a href="./5_1_5_Disabling_Breakpoints.md">Disabling Breakpoints</a></li>
                    <li><a href="./5_1_6_Break_Conditions.md">Break Conditions</a></li>
                    <li><a href="./5_1_7_Breakpoint_Commands.md">Breakpoint Commands</a></li>
                    <li><a href="./5_1_8_Dynamic_Printf.md">Dynamic Printf</a></li>
                    <li><a href="./5_1_9_Saving_Breakpoints.md">Saving Breakpoints</a></li>
                    <li>Static Probe Points</li>
                    <li><a href="./5_1_11_Breakpoint_Errors.md">Errors in Breakpoint</a></li>
                    <li>Breakpoint-related Warning</li>
                </ol>
            </li>
            <li><a href="./5_2_Continuing_and_Stepping.md">Continuing and Stepping</a></li>
            <li><a href="./5_3_Skipping_Over_Functions_and_Files.md">Skipping Over Functions and Files</a></li>
            <li><a href="./5_4_Signals.md">Signals</a></li>
            <li>Stopping and Starting Multi-Thread Programs</li>
        </ol>
    </li>
    <li><a href="./6_Running_Programs_Backward.md">Running Programs Backward</a></li>
    <li><a href="./7_Recording_Inferiors_Execution_and_Replaying_it.md">Recording Inferior's Execution and Replaying It</a></li>
    <li>
        <a href="./8_Examining_the_Stack.md">Examining the Stack</a>
        <ol type="1">
            <li><a href="./8_1_Stack_Frames.md">Stack Frames</a></li>
            <li><a href="./8_2_Backtrace.md">Backtrace</a></li>
            <li><a href="./8_3_Selecting_a_Frame.md">Selecting a Frame</a></li>
            <li><a href="./8_4_Information_About_a_Frame.md">Information about a Frame</a></li>
            <li>Applying a Command to Several Frames</li>
            <li>Management of Frame Filters</li>
        </ol>
    </li>
    <li>
        <a href="./9_Examining_Source_Files.md">Examining Source Files</a>
        <ol type="1">
            <li><a href="./9_1_Printing_Source_Lines.md">Printing Source Lines</a></li>
            <li>
                <a href="./9_2_Specifying_a_Location.md">Specifying a Location</a>
                <ol type="1">
                    <li><a href="./9_2_1_Linespec_Locations.md">Linespec Locations</a></li>
                    <li><a href="./9_2_2_Explicit_Locations.md">Explicit Locations</a></li>
                    <li><a href="./9_2_3_Address_Locations.md">Address Locations</a></li>
                </ol>
            </li>
            <li><a href="./9_3_Editing_Source_Files.md">Editing Source Files</a></li>
            <li><a href="./9_4_Searching_Source_Files.md">Searching Source Files</a></li>
        </ol>
    </li>
    <li>
        <a href="./10_Examining_Data.md">Examining Data</a>
        <ol type="1">
            <li><a href="./10_1_Expressions.md">Expressions</a></li>
            <li><a href="./10_2_Ambiguous_Expressions.md">Ambiguous Expressions</a></li>
            <li><a href="./10_3_Program_Variables.md">Program Variables</a></li>
            <li><a href="./10_4_Artificial_Arrays.md">Artificial Arrays</a></li>
            <li><a href="./10_5_Output_Formats.md">Output Formats</a></li>
            <li><a href="./10_6_Examining_Memory.md">Examining Memory</a></li>
            <li><a href="./10_7_Automatic_Display.md">Automatic Display</a></li>
            <li><a href="./10_8_Print_Settings.md">Print Settings</a></li>
            <li>
                <a href="./10_9_Pretty_Printing.md">Pretty Printing</a>
                <ol type="1">
                    <li><a href="./10_9_1_Pretty_Printer_Introduction.md">Pretty Printer Introduction</a></li>
                    <li><a href="./10_9_2_Pretty_Printer_Example.md">Pretty Printer Example</a></li>
                    <li><a href="./10_9_3_Pretty_Printer_Commands.md">Pretty Printer Commands</a></li>
                </ol>
            </li>
            <li><a href="./10_10_Value_History.md">Value History</a></li>
            <li>Convenience Variables</li>
            <li>Convenience Functions</li>
            <li><a href="./10_13_Registers.md">Register</a></li>
            <li>Floating Point Hardware</li>
            <li>Vector Unit</li>
            <li><a href="./10_16_OS_Aux_Info.md">OS Auxilary Information</a></li>
            <li><a href="./10_17_Memory_Region_Attributes.md">Memory Region Attributes</a></li>
            <li><a href="./10_18_Copy_Between_Memory_and_a_File.md">Copy Between Memory and a File</a></li>
            <li><a href="./10_19_Core_Files.md">Core Files</a></li>
            <li>Character Sets</li>
            <li>Searching Memory</li>
            <li><a href="./10_22_Search_Memory.md">Search Memory</a></li>
        </ol>
    </li>
    <li>
        <a href="./11_Debugging_Optimized_Code.md">Debugging Optimized Code</a>
    </li>
    <li>
        C Preprocessor Macros
    </li>
    <li>
        <a href="./13_Tracepoints.md">Tracepoints</a>
    </li>
    <li>
        Debugging Programs That Use Overlays
    </li>
    <li>
        <a href="./15_Using_GDB_with_Different_Languages.md">Using GDB with Different Languages</a>
    </li>
    <li>
        <a href="./16_Examining_the_Symbol_Table.md">Examining the Symbol Table</a>
    </li>
    <li>
        <a href="./17_Altering_Execution.md">Altering Execution</a>
        <ol>
            <li><a href="./17_Altering_Execution.md">Assignment</a></li>
            <li><a href="./17_Altering_Execution.md">Jumping</a></li>
            <li><a href="./17_Altering_Execution.md">Signaling</a></li>
            <li><a href="./17_Altering_Execution.md">Returning</a></li>
            <li><a href="./17_Altering_Execution.md">Calling</a></li>
            <li><a href="./17_Altering_Execution.md">Patching</a></li>
            <li>Compiling and Injecting code</li>
        </ol>
    </li>
    <li>
        <a href="./18_GDB_Files.md">GDB Files</a>
        <ol>
            <li><a href="./18_GDB_Files.md">Files</a></li>
            <li>File caching</li>
            <li><a href="./17_Altering_Execution.md">Separate Debug File</a></li>
            <li>MiniDebugInfo</li>
            <li>Index Files</li>
            <li>Symbol Errors</li>
            <li>Data Files</li>
        </ol>
    </li>
    <li>
        <a href="./19_Debugging_Target.md">Specifiying a Debugging target</a>
        <ol>
            <li><a href="./19_Debugging_Target.md">Byte Order</a></li>
        </ol>
    </li>
    <li>Debugging Remote Programs</li>
    <li>Configuration-Specific Information</li>
    <li>Controlling GDB</li>
    <li>Extending GDB</li>
    <li>Command Interpreters</li>
    <li>
        <a href="./25_GDB_TUI.md">GDB TUI</a>
        <ol>
            <li><a href="./25_GDB_TUI.md">Overview</a></li>
            <li><a href="./25_GDB_TUI.md">Keys</a></li>
            <li>Single Key Mode</li>
            <li><a href="./25_GDB_TUI.md">Commands</a></li>
            <li><a href="./25_GDB_TUI.md">Configurations</a></li>
        </ol>
    </li>
</ol>
