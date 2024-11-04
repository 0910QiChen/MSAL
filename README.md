# MSAL in .NET Web API
1. Go to Azure Portal -> Microsoft Entra ID
2. Add New Application -> Register your Web API
3. Copy the Directory (tenant) ID and Application (client) ID for Web API appsetting.json
4. Under Manage -> Expose an API -> Add Scope, give it a name and who has access to it -> Save
5. Under Manage -> Authentication -> Add a Platform, choose any client application or test application for the Authentication test (this will need a redirect URI)
6. Under Manage -> Certificates & secrets, add any secrets for authentication purpose (this step isn't important)
7. Time for .NET Web API Configuration
   1. use CLI to build your dotnet project
   2. install two packages for authentication purposes:
      - Microsoft.AspNetCore.Authentication.JwtBearer
      - Microsoft.Identity.Web
   3. configure AzureAD in appsetting.json as
      "AzureAd":
        {"Instance": "https://login.microsoftonline.com/",
        "TenantId": "xxx",
        "ClientId": "xxx",
        "Scope": "xxx"
      }
   4. add authentication service in Program.cs as
      builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
          .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAd"));
   5. use authentication service in Program.cs as
      app.UseAuthentication();
