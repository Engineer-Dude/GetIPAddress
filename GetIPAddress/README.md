# GetIPAddress

This project starts with an Empty Blazor Server project and adds a few lines to allow the accessing of the user's IP Address.

1. Add the class BlazorAppContext.cs and add a property to it called CurrentUserIP.  This holds the value that is returned.

2. Add the following to Program.cs:
```
	builder.Services.AddScoped<BlazorAppContext>();
	builder.Services.AddHttpContextAccessor();
```  

3. Add the following to App.razor

	```@* Add this block to get the IP Address from the context *@
	@inject IHttpContextAccessor httpContextAccessor
	@inject BlazorAppContext blazorAppContext
	@{
		var remoteIpAddress = httpContextAccessor?.HttpContext?.Connection?.RemoteIpAddress?.ToString() ?? "";
		blazorAppContext.CurrentUserIP = remoteIpAddress;
	}
	```
4. Add the following to Index.razor to access the value and display it on the page
```
	@inject BlazorAppContext blazorAppContext
	<p>The IP Address is @blazorAppContext.CurrentUserIP</p>
```

