---
layout: post
title: .NET - Impersonate local user on another machine
category: Dev
tags: [.NET, C#]
---

Usually, in .NET in order to impersonate a local user on another machine (e.g. for copying a file or for read a folder), the same credential are copied on the machine that require access.

It can be used a method like the following:

```csharp
 private Impersonate(string domain, string username, string password, LogonType logonType, LogonProvider logonProvider)
        {
			IntPtr handle;
			var ok = NativeMethods.LogonUser(username, domain, password, (int)logonType, (int)logonProvider, out handle);
			if (!ok)
			{
				var errorCode = Marshal.GetLastWin32Error();
				throw new ApplicationException(string.Format("Could not impersonate the elevated user.  LogonUser returned error code {0}.", errorCode));
			}

			_handle = new SafeTokenHandle(handle);
			_context = WindowsIdentity.Impersonate(_handle.DangerousGetHandle());            
        }
```

that use this Windows API:

```csharp
[DllImport("advapi32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
internal static extern bool LogonUser(String lpszUsername, String lpszDomain, String lpszPassword, int dwLogonType, int dwLogonProvider, out IntPtr phToken);
```	 

and called in this way:

```csharp
    using (Impersonate.LogonUser(
        ".",
        "todev1.domain.com\admin",
        "Test123_",
        LogonType.Interactive,
		LogonProvider.Default))
    {

    } 
```	 

Where LogonType is an enum of values taken from here: https://msdn.microsoft.com/en-us/library/windows/desktop/aa378184(v=vs.85).aspx

Honestly this is not the best because of, almost, two points:
 - each machine on the farm must have the credentials set, if missed the application break
 - if, for security reasons the password changes, it must be changed in all the "client" machines

The docs are a litlle foggy, but it's possible to impersonate a local user without replicate it, the magic is the combination of LogonType and LogonProvider.

The LOGON32_LOGON_NEW_CREDENTIALS has a magic description:
> This logon type allows the caller to clone its current token and specify new credentials for outbound connections. The new logon session has the same local identifier but uses different credentials for other network connections.
This logon type is supported only by the LOGON32_PROVIDER_WINNT50 logon provider.

If you call the impersonation method :

```csharp
using (Impersonate.LogonUser(true,
    "todev1.domain.com",
    "admin",
    "Test123_",
    LogonType.NewCredentials,
    LogonProvider.WinNT50))
{

}
```

and the impersonation will work great!