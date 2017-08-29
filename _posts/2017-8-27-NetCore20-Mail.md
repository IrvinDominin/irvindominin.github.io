---
layout: post
title: .NET Core 2.0 - Send an e-mail
category: Dev
tags: [.NET Core]
---

In .NET Core 1.x the SMTP client code was not ported, that is true until of .NET Core 2.0.

With .NET Core 2.0, the interfaces are identical to the classical present on the full framework. Consider that following code is in .NET Core 2.0.

```csharp
SmtpClient client = new SmtpClient(<your server>);
client.UseDefaultCredentials = false;
client.Credentials = new NetworkCredential(<user>, <pwd>);
 
MailMessage mailMessage = new MailMessage();
mailMessage.From = new MailAddress("noreply@myblog.io");
mailMessage.To.Add(<to>);
mailMessage.Body = "Wow, a .NET Core e-mail";
mailMessage.Subject = "New e-mail";
client.Send(mailMessage);
```

Essentially, if you have the code that could send an e-mail using SMTP in the full framework you can use it on .NET Core.

But, Microsoft is not a big fan of SmtpClient class, because: 
> SmtpClient and its network of types are poorly designed' so it's reccomended to use an external library like <a href="https://github.com/jstedfast/MailKit">MailKit</a>

So here is the code to send an e-mail using MailKit:

```csharp
var message = new MimeMessage ();
message.From.Add(new MailboxAddress("No-reply", "noreply@myblog.io"));
message.To.Add(new MailboxAddress(<to>, <to>));
message.Subject = "New e-mail";
message.Body = new TextPart("plain") {
Text = "Wow, a MailKit e-mail";

using (var client = new SmtpClient ()) {
	// For demo-purposes, accept all SSL certificates (in case the server supports STARTTLS)
	client.ServerCertificateValidationCallback = (s,c,h,e) => true;

	client.Connect (<your server>, <your port>, false);

	// Note: since we don't have an OAuth2 token, disable
	// the XOAUTH2 authentication mechanism.
	client.AuthenticationMechanisms.Remove ("XOAUTH2");

	// Note: only needed if the SMTP server requires authentication
	client.Authenticate(<user>, <pwd>);

	client.Send (message);
	client.Disconnect (true);
}
```