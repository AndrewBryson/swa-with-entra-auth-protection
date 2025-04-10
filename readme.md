# Custom Entra authentication with Azure Static Web Apps (SWA)

- Custom auth in SWA requires a Standard Hosting plan.
- Configuration specified in: `src/staticwebapp.config.json`
   - You must configure the `openIdIssuer` to match your own tenant ID.
   - The `AZURE_CLIENT_ID` and `AZURE_CLIENT_SECRET_APP_SETTING_NAME` configuration reference keys you must specify in your SWA [Environment Variables](https://learn.microsoft.com/en-us/azure/static-web-apps/application-settings). 
- Uses the custom authentication feature of SWA: https://learn.microsoft.com/en-us/azure/static-web-apps/authentication-custom?tabs=aad%2Cinvitations

- Entra App Registration:
   - An Entra App Registration must be created: https://learn.microsoft.com/en-us/azure/app-service/configure-authentication-provider-aad?tabs=workforce-configuration
   - The App Registration is configured with:
        - A "platform" of `Web` with a redirect URL of `https://<Your-SWA-FQDN/.auth/login/aad/callback`
        - Under `Select the tokens you would like to be issued...` select the option: `ID tokens (used for implicit and hybrid flows)`.  The token requirements will vary depending on your use case.

   - Optionally, configuring the App to restrict to a set of users: https://learn.microsoft.com/en-us/entra/identity-platform/howto-restrict-your-app-to-a-set-of-users
   - Optionally, grant tenant-wide admin consent to the App: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/grant-admin-consent?pivots=portal

- General: Microsoft Learn module for SWA with authentication: https://learn.microsoft.com/en-us/training/modules/publish-static-web-app-authentication/