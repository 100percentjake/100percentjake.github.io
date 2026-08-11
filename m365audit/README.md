# M365 Audit

Static, delegated Microsoft Graph audit dashboard. Tenant data is collected directly in the administrator's browser. There is no application backend. CSV and offline HTML exports are explicit local downloads.

## App registration

The public-client app registration identified by `CLIENT_ID` in `index.html` must be configured as a single-page application with the deployed URL as an exact redirect URI. It requests these delegated Microsoft Graph permissions:

- `User.Read.All`
- `Group.Read.All`
- `GroupMember.Read.All`
- `RoleManagement.Read.Directory`
- `Reports.Read.All`
- `AuditLog.Read.All`
- `MailboxSettings.Read`
- `Organization.Read.All`
- `IdentityRiskyUser.Read.All`
- `SharePointTenantSettings.Read.All`

Grant tenant-wide admin consent before routine use. The signed-in operator still needs roles supported by each API. Global Reader, Reports Reader, Security Reader, and SharePoint Administrator cover the optional reporting areas more narrowly than routine use of Global Administrator.

## Collection semantics

Every optional source is tracked as `loaded`, `partial`, `permission-denied`, `throttled`, `failed`, or `not-applicable`. A failed source is displayed and exported as **Unknown**, never as an empty collection or a passing result.

Graph collection requests honor `Retry-After`, use exponential backoff for transient failures, follow pagination, and batch group and mailbox subrequests in groups of 20.

## Supported security checks

- MFA registration and registered method summary
- Entra risky users (requires Entra ID P2)
- Guest invitation, inactivity, and direct collected group-membership review
- Inbox forwarding and redirect rules
- SharePoint/OneDrive tenant sharing capability and domain restrictions
- User, directory-role, license, group, ownership, membership, and activity reporting

## Explicit limitations

Microsoft Graph does not expose authoritative Exchange recipient type, mailbox-level `ForwardingSmtpAddress`, mailbox delegates, or Exchange transport rules to this browser collector. Those checks are shown as not applicable and require Exchange Online PowerShell. Accounts matching the old shared-mailbox heuristic are labeled **Possible Shared Mailbox** and must be verified in Exchange.

License overlap findings use the tenant's live `subscribedSkus` service-plan inventory and each assignment's disabled plans. They are review candidates, not removal instructions: billing, prerequisites, group licensing, and contract terms are outside Graph's assignment data.

The vendored `msal-browser.min.js` is Microsoft `@azure/msal-browser` 5.17.3. Its license is in `MSAL-LICENSE.txt`.
