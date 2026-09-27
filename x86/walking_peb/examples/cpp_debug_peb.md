/*
===============================================================================
 x86 Windows PEB BeingDebugged Teaching Demonstration
===============================================================================
 PURPOSE
 -------
 
 This program demonstrates how a 32-bit Windows process can locate its
 Process Environment Block (PEB) and inspect the BeingDebugged field.
 Students can use this program with x32dbg to observe:
cl /EHsc /Zi /Od peb_demo.cpp /Fe:peb_demo.exe
        TEB
         |
         | FS:[0x30]
         v
        PEB
         |
         | +0x02
         v
    BeingDebugged

 When a debugger is attached, the BeingDebugged byte is normally:

        0x01 = debugger indicated
        0x00 = debugger not indicated

 The program then changes the BeingDebugged byte from 1 to 0 so students
 can observe how changing this PEB field affects this particular check.

 IMPORTANT
 ---------
 Compile this program as x86 / 32-bit.

 The example intentionally uses the x86 FS register.

 On x86 Windows:

        FS:[0x30] -> PEB

 This is different from the normal x64 mechanism, which uses GS.
===============================================================================
 OPTION 1 - VISUAL STUDIO
===============================================================================
 1. Open Visual Studio.
 2. Create:
        Create a new project
             ->
        Console App
             ->
        C++
 3. Replace the generated source code with this file.
 4. Select:

        Build
          ->
        Configuration Manager

 5. Set:
        Active solution platform: x86
    DO NOT compile this exercise as x64.
 6. For the easiest debugging demonstration, select:
        Debug
        x86
 7. Build the program:
        Build
         ->
        Build Solution

    Keyboard shortcut:

        Ctrl + Shift + B

 8. The executable will normally be under something similar to:

        <project>\Debug\
        <project>\x86\Debug\

 9. Open the resulting EXE in x32dbg.
===============================================================================
 OPTION 2 - VISUAL STUDIO DEVELOPER COMMAND PROMPT
===============================================================================

 Open the:

        x86 Native Tools Command Prompt for VS

 Change to the directory containing this source file.

 If the source is named:

        peb_demo.cpp

 Compile with:

        cl /EHsc /Zi /Od peb_demo.cpp /Fe:peb_demo.exe

 Important compiler options:

        /EHsc    Standard C++ exception handling
        /Zi      Include debugging information
        /Od      Disable optimization
        /Fe      Specify output EXE filename

 /Od is particularly useful for this classroom exercise because compiler
 optimization can make the generated assembly harder for beginning students
 to follow.


===============================================================================
 EXPECTED x86 PEB STRUCTURE
===============================================================================

 Simplified view:

        FS:[0x30]
            |
            v
      +-----------------------+
      |          PEB          |
      +-----------------------+
 +00  | InheritedAddressSpace |
 +01  | ReadImageFile...      |
 +02  | BeingDebugged         | <---- FIELD USED HERE
 +03  | BitField              |
      | ...                   |
      +-----------------------+

 The important relationship for this exercise is:

        FS:[0x30]       = address of PEB

        PEB + 0x02      = address of BeingDebugged


===============================================================================
 CLASSROOM WALKTHROUGH
===============================================================================

 When debugging this program, students should identify:

    1. The FS register
    2. FS:[0x30]
    3. The address of the PEB
    4. PEB + 0x02
    5. The BeingDebugged byte
    6. Its value before modification
    7. Its value after modification

 This is an intentionally small educational example designed to make the
 PEB relationship visible in a debugger.

===============================================================================
*/

#include <Windows.h>
#include <iostream>
#include <intrin.h>

// Tell the Microsoft compiler that we want to use this intrinsic.
#pragma intrinsic(__readfsdword)


int main()
{
    std::cout << "============================================\n";
    std::cout << " x86 PEB BeingDebugged Teaching Demo\n";
    std::cout << "============================================\n\n";
    // -----------------------------------------------------------------
    // STEP 1: Locate the PEB
    // -----------------------------------------------------------------
    //
    // In a 32-bit Windows process, the FS segment register provides
    // access to the Thread Environment Block (TEB).
    //
    // The pointer at:
    //
    //              FS:[0x30]
    //
    // points to the Process Environment Block (PEB).
    //
    // Conceptually, students may encounter assembly similar to:
    //
    //              MOV EAX, DWORD PTR FS:[30h]
    //
    // After that instruction:
    //
    //              EAX = address of PEB
    //
    DWORD pebAddress = __readfsdword(0x30);
    // Convert the PEB address into a byte pointer.
    //
    // Using BYTE* makes the next operation easy because adding 2
    // advances exactly two bytes.
    BYTE* peb = reinterpret_cast<BYTE*>(pebAddress);
    // -----------------------------------------------------------------
    // STEP 2: Locate BeingDebugged
    // -----------------------------------------------------------------
    //
    // BeingDebugged is located at offset:
    //
    //              PEB + 0x02
    //
    // Therefore:
    //
    //              beingDebugged = PEB address + 2 bytes
    //
    BYTE* beingDebugged = peb + 0x02;
    // -----------------------------------------------------------------
    // STEP 3: Display the addresses
    // -----------------------------------------------------------------
    std::cout << "PEB Address:          0x"
              << std::hex
              << pebAddress
              << "\n";
    std::cout << "BeingDebugged Address: 0x"
              << std::hex
              << reinterpret_cast<DWORD>(beingDebugged)
              << "\n";
    // -----------------------------------------------------------------
    // STEP 4: Read BeingDebugged
    // -----------------------------------------------------------------
    //
    // Expected values:
    //
    //              00 = debugger not indicated
    //              01 = debugger indicated
    //
    std::cout << "BeingDebugged Value:   "
              << std::dec
              << static_cast<int>(*beingDebugged)
              << "\n\n";
    // -----------------------------------------------------------------
    // STEP 5: Check the value
    // -----------------------------------------------------------------

    if (*beingDebugged != 0)
    {
        std::cout << "[+] Debugger detected through PEB!\n";
    }
    else
    {
        std::cout << "[-] PEB does not indicate a debugger.\n";
    }

    // Pause here.
    //
    // This is a useful place for students to examine:
    //
    //              FS:[30]
    //
    // and:
    //
    //              PEB + 02
    //

    std::cout << "\nPress ENTER to clear BeingDebugged...";
    std::cin.get();


    // -----------------------------------------------------------------
    // STEP 6: Change BeingDebugged
    // -----------------------------------------------------------------
    //
    // Change:
    //
    //              PEB + 0x02
    //
    // from:
    //
    //              01
    //
    // to:
    //
    //              00
    //
    // This demonstrates bypassing this specific PEB-based check.
    //

    *beingDebugged = 0;


    // -----------------------------------------------------------------
    // STEP 7: Read the value again
    // -----------------------------------------------------------------

    std::cout << "\nBeingDebugged after change: "
              << std::dec
              << static_cast<int>(*beingDebugged)
              << "\n";


    if (*beingDebugged == 0)
    {
        std::cout << "[+] BeingDebugged flag has been cleared.\n";
    }


    // Keep the program open so students can continue examining memory.

    std::cout << "\nPress ENTER to exit...";
    std::cin.get();

    return 0;
}
