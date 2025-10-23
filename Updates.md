# Modern Workplace Concierge: Overview and Changes

## What the Repository Has
The **Modern Workplace Concierge** is an open-source ASP.NET MVC web application designed to simplify Microsoft 365 (formerly Office 365) administration tasks, particularly for Enterprise Mobility + Security (EM+S) features. It serves as a helper tool for IT professionals managing Intune (Microsoft Endpoint Manager) and Conditional Access policies. Key capabilities include:

- **Intune Management**:
  - Export/import device configurations, compliance policies, and settings.
  - Deploy and manage PowerShell scripts and Win32 app detection scripts.
  - Handle offline Autopilot profiles for device enrollment.

- **Conditional Access**:
  - Import/export policies.
  - Deploy baseline security policies (e.g., for MFA, device compliance).
  - Generate documentation and reports in CSV format.

- **Other Features**:
  - Migrate Trello boards to Microsoft Planner.
  - Self-hosting support with Azure deployment templates.
  - User authentication via Microsoft Graph API, with role-based access (e.g., AdvancedUser).

The app uses the Microsoft Graph Beta API, supports multi-tenant Azure AD apps, and includes CI/CD pipelines (Azure DevOps), SignalR for real-time notifications, and PWA (Progressive Web App) features. It's archived and no longer actively maintained, but forkable for custom use.

## Changes Made
We made targeted updates to personalize and extend the app:

1. **Name Replacement (Footprint Update)**:
   - **Files Modified**:
     - `ModernWorkplaceConcierge/Views/About/Index.cshtml`: Updated presenter name and tech blog reference from "Nicola Suter" to "Chrls.tjokro".
     - `ModernWorkplaceConcierge/Views/Shared/_Layout.cshtml`: Updated footer presenter link from "Nicola Suter" to "Chrls.tjokro".
   - **Files Unchanged**: `LICENSE.md` retained "Nicola Suter" as the original copyright holder.

2. **Added MFA Test Feature (Maester MT.1007 Integration)**:
   - **Controller Update**: `ConditionalAccessController.cs` – Added `TestMFAForAllUsers` (view action) and `RunTestMFAForAllUsers` (async test execution action).
   - **View Creation**: `TestMFAForAllUsers.cshtml` – New page with a "Run Test" button for user interaction.
   - **Menu Addition**: Updated `_Layout.cshtml` to include "Test MFA for All Users" in the Conditional Access dropdown.
   - **Functionality**: The test checks for at least one enabled Conditional Access policy requiring MFA for all users (based on Maester's MT.1007 test). It queries policies via Microsoft Graph, verifies conditions (`includeUsers: "All"`, `grantControls.builtInControls: "mfa"`), and reports PASS/FAIL via SignalR notifications.

## Why These Changes
- **Name Replacement**: To rebrand the app from its original creator ("Nicola Suter") to a new maintainer ("Chrls.tjokro"), updating public-facing text while respecting copyright in the license.
- **MFA Test Feature**: To enhance the app's Conditional Access tools by adding compliance checking for MFA policies, aligning with security best practices from Maester (a PowerShell-based testing framework for Microsoft 365). This provides users with an easy way to audit and ensure MFA enforcement across their tenant, improving the app's utility for security-focused admins. The test is simple, real-time, and integrates seamlessly with the existing UI and API calls.

These changes maintain the app's core functionality while making it more personalized and feature-rich. No breaking changes were introduced, and the app remains deployable via the provided Azure templates.
