# Win32Methods

Provides an set of API methods from win32 instead of P/invoke using DllImport attribute. Not meant to be an Interop.  you can now have an class that contains this functions and make it easier for you, e.g Window class is managing a window containing the exported functions to modify it as property and methods. The link is:  https://www.nuget.org/packages/Win32Methods

here's another exmample: LibraryManager class is the base class for performing platform invoke actions.

Example:


// Loading the library with the targeten library called user32. And disposes it at the end of the code. Because it loads the library. so we should free it to not get memory leak.
using LibraryManager user32 = new("user32.dll");
// getting a function pointer called MessageBoxW in the user32 library and converting it to the function pointer.
var msgBox = (delegate* unmanaged[Stdcall]<IntPtr, IntPtr, IntPtr, uint, IntPtr>)user32.GetExportedFunctionPointer("MessageBoxW");
// now we are calling the messageBox function pointer using The Marshal to marshal to string to unicode string. LPCWSTR in C++.
msgBox(IntPtr.Zero, Marshal.StringToHGlobalUni("Hello, world!"), Marshal.StringToHGlobalUni("My first message box!"), 0);
// And that's all of this documentation.
