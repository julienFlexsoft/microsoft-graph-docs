# Authorization and the security API in Microsoft Graph

Security data accessible via the security API in Microsoft Graph is sensitive and is protected by both permissions and Azure Active Directory (Azure AD) roles.

The security API supports two types of authorization:

- **Application-level authorization** - There is no signed-in user (for example, a SIEM scenario). The permissions granted to the application determine authorization. 
    >**Note:** This option can also support cases where Role-Based Access Control (RBAC) is managed by the application.
- **User delegated authorization** - A user who is a member of the Azure AD tenant is signed in. The user must be a member of an Azure AD Limited Admin role - either Security Reader or Securty Administrator - in addition to the application having been granted the required permissions.

If you're calling the security API from Graph Explorer:

- The Azure AD tenant admin must explicitly grant consent for the requested permissions to the Graph Explorer application.
- The user must be a member of the Security Reader Limited Admin role in Azure AD (either Security Reader or Security Administrator).

>**Note**: Graph Explorer does not support application-level authorization.

If you're calling the security API from a custom or your own application:

- The Azure AD tenant admin must explicitly grant consent to your application. This is required both for application-level authorization and user delegated authorization.
- If you're using user delegated authorization, the user must be a member of the Security Reader or Security Administrator Limited Admin role in Azure AD.

## Managing authorization in security API client applications

Security data provided via the security API in Microsoft Graph is sensitive and must be protected by appropriate authentication and authorization mechanisms. The following table lists the steps to register and create a client application that can access the security API.

| **Who** | **Action** |
|:---------------------|:------------------|
|Application developer or owner|Register the application as an enterprise application.|
|Tenant admin|Grant permissions to the application.|
|Tenant admin|Assign roles to users.|
|Application developer|Sign in as the user and use the application to access the security API.|

Application registration only defines which permissions the application needs in order to run. It does NOT grant these permissions to the application.

The Azure AD tenant administrator MUST explicitly grant the permissions to the application. This must be done per tenant and must be *performed every time* the application permissions are changed in the application registration portal.

For example, assume that you have an application, two Azure AD tenants, **T1** and **T2**, and two permissions, **P1** and **P2**. The following is the authorization process:

- The application registers to require permission **P1**.
- When users in tenant **T1** get an Azure AD token for this application, the token does not contain any permissions.
- The Azure AD admin of tenant **T1** explicitly grants permissions to the application. When users in tenant **T1** get an Azure AD token for the application, it will contain permission **P1**.
- When users in tenant **T2** get an Azure AD token for the application, the token does not contain any permissions - because the admin of tenant **T2** did not yet grant permissions to the application. Permission must be granted *per tenant* and *per application*.
- The application has its registration changed to now require permissions **P1** and **P2**.
- When users in tenant **T1** get an Azure AD token for the application, it only contains permission **P1**. Permissions granted to an application are recorded as snapshots of what was granted - they *do not change automatically* after the application registration (permission) changes.
- The admin of tenant **T2** grants permissions **P1** and **P2** to the application. Now, when users in tenant **T2** get an Azure AD token for the application, the token will contain permissions **P1** and **P2**.

>**Note**: The Azure AD tokens for the application in tenant **T1** and the application in tenant **T2** contain different permissions, because each tenant admin has granted different permissions to the application.

- To make the application work again in tenant **T1**, the admin of tenant **T1** must explicitly grant permissions **P1** and **P2** to the application.

## Register an application in the Azure AD v2.0 endpoint

To register an application to the Azure AD v2.0 endpoint, you'll need:

- **Application name** - A string used for the application name.
- **Redirect URL** - The URL where the authentication response from Azure AD is sent. To start, you can use the test client web app homepage.
- **Required Permissions** - The permissions that your application requires to be able to call Microsoft Graph.

To register your application:

1. Go to https://apps.dev.microsoft.com/ and sign in.
    >**Note**: You don't have to be a tenant admin. You will be redirected to the **My applications** list.
2. Choose **Add an app**, and enter an **Application Name** to create a new application.
3. On the registration page for the new application, choose **Add Platform** > **Web**. In the **Redirect URL** field, enter the redirect URL.
4. In the **Microsoft Graph Permissions** section, under **Delegated Permissions**, choose **Add**. In the dialog box, choose the required permissions. For a list of permissions, see [Security permissions](../concepts/permissions_reference.md#security-permissions).

    >The security API requires the SecurityEvents.Read.All scope for GET queries, and the SecurityEvents.ReadWrite.All scope for PATCH/POST queries.

5. Choose **Save**.

Save the following information:

- Application ID
- Redirect URL
- List of required permissions

For more information, see [Register your app with the Azure AD v2.0 endpoint](../concepts/auth_register_app_v2.md).

## Granting permissions to an application

Application registration only defines which permission the application requires - it does not grant these permissions to the application. An Azure AD tenant administrator must explicitly grant these permissions by making a call to the admin consent endpoint. For details, see [Using the admin consent endpoint](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

To grant permissions to an application, you'll need:

- **Application ID** - The application ID from application registration portal.
- **Redirect URL** - The string you set in the application registration portal for authentication response.

To grant the permissions:

- In a text editor, create following URL string:

    `https://login.microsoftonline.com/common/adminconsent?client_id=<Application Id>&state=12345&redirect_uri=<Redirect URL>`

- In a web browser, go to this URL, and sign in as a tenant administrator. The dialog box shows the list of permission the application requires, as specified in the application registration portal. 
Choose **OK** to grant the application these permissions.

> **Note:** This step grants permissions to the application - not to users. This means that all users belonging to the Azure AD tenant that use this application will be granted these permissions - even non-admin users.

## Assigning Azure AD roles to users

After an application is granted permissions, everyone with access to the application (that is, members of the Azure AD tenant) will receive the granted permissions. To further protect sensitive security data, the security API also requires users to be assigned the Azure AD **Security Reader** role. For details, see [Assigning administrator roles](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles-azure-portal) and [Assign a user to adminstrator roles](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-assign-role-azure-portal).

>**Note:** You must be a tenant admin to perform this step.

To assign roles to users:

- Sign in to the [azure portal](https://portal.azure.com/#@isgdemodev.onmicrosoft.com/dashboard/private/76e81922-1bdf-455e-bdbb-33ff73765011) (http://portal.azure/com).
- In the menu, select **Azure Active Directory** > **Users**.
- Select the name of the user.
- Select **Manage** > **Directory role**.
- Select **Limited administrator**, and choose the **Security reader** check box.
- Choose **Save**.

## Create an authentication code

To create an authentication code, you'll need:

- **Application ID** - The application ID from application registration portal.
- **Redirect URL** - The URL where the authentication response from Azure AD is sent. To start, you can use http://localhost or the test client web app homepage.
- **Application Key** (optional) - The key of the application. This applies when you're developing an application that will use application-only authentication code (that is, will not support user delegated authentication).

The following table lists resources that you can use to create an authentication code.

|**Type of application**|**Authentication library**|
|------------------------|----------------------------|
|[Desktop apps - iOS](https://docs.microsoft.com/en-us/azure/active-directory/develop/guidedsetups/active-directory-ios)|[MSAL.framework: Microsoft Authentication Library Preview for iOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|
|[Desktop apps - Android](https://docs.microsoft.com/en-us/azure/active-directory/develop/guidedsetups/active-directory-android)|[Microsoft Authentication Library (MSAL)](http://javadoc.io/doc/com.microsoft.identity.client/msal)|
|[Desktop apps - .Net](https://docs.microsoft.com/en-us/azure/active-directory/develop/guidedsetups/active-directory-windesktop)|[Microsoft Authentication Library (MSAL)](https://www.nuget.org/packages/Microsoft.Identity.Client)|
|[Web apps - JavaScript SPA](https://docs.microsoft.com/en-us/azure/active-directory/develop/guidedsetups/active-directory-javascriptspa)|[Microsoft Authentication Library for JavaScript Preview](https://github.com/AzureAD/microsoft-authentication-library-for-js)|
|[Web apps - .NET Web Server](https://docs.microsoft.com/en-us/azure/active-directory/develop/guidedsetups/active-directory-aspnetwebapp)|OpenIdConnection, Cookies, SystemWeb|
|[Web apps - NodeJS Web App](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-devquickstarts-node-web)||

For applications that don't use any of the existing libraries, see [Get access on behalf of a user](../concepts/auth_v2_user.md).

1. Get a code from Azure AD. The query to call contains parameter for Application ID, Redirect URl, and **required permissions**.
2. Use the code to get an access token.

If you use OpenId Connect library, see [Authenticate using Azure AD and OpenID Connect](https://docs.microsoft.com/en-us/azure/architecture/multitenant-identity/authenticate) and call `app.UseOpenIdConnectAuthentication()`.

>**Note:** If you're requesting user delegated authentication tokens, the parameter for the library is **Requested Scopes**. Use User.Read for this parameter instead of what the registered application requires. The **Requested Scopes** parameter does NOT affect the permissions contained in the returned authentication tokens. These are determined by the permissions that the tenant admin granted the application.

For example, if you're using the .NET MSAL library, call the following:

`var accessToken = (await client.AcquireTokenAsync(scopes)).AccessToken;`

>**Note:** This example should use the least privileged permission, such as User.Read. However, the returned access token can contain permissions that were granted by the tenant admin for the current user tenant, such as User.Read.All or User.ReadWrite.All.

A token (string) is returned by Azure AD that contains your authentication information and the permissions required by the application. Assign this token to the HTTP header as a bearer token, as shown in the following example.

`request.Headers.Authorization = new AuthenticationHeaderValue("bearer", accessToken);`

Microsoft Graph will validate the information contained in this token and grant, or reject, access.

To view claims contained in the returned token, use NuGet library System.IdentityModel.Tokens.Jwt.

`JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler();`</br>
`var securityToken = tokenHandler.ReadToken(accessToken) as JwtSecurityToken;`

The response from Microsoft Graph contains a header called client-request-id, which is a GUID. If access is denied, please specify this GUID when seeking support, so we can help investigate the cause of this authentication failure.