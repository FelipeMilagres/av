Hello Swapneel,

Thank you for your guidance.

I would like to clarify one additional point regarding our environment. We have a dedicated IP configured for our organization, and I would like to confirm whether this same IP is used for network requests generated during App Automation executions on iOS devices.

Could you please confirm:

- Whether our dedicated proxy IP is automatically used for iOS App Automation sessions or whether the `dedicatedProxy: true` capability must be explicitly enabled in our test configuration.
- Whether any additional configuration is required to ensure that application requests are routed through our dedicated IP during automated test execution.
- Whether requests can still originate from TestMu AI's public IP ranges when a dedicated IP is configured but not explicitly enabled for the session.

I have already enabled `network: true` in our test configuration and am running additional tests to collect network logs for further investigation with our Information Security team.

We would appreciate your confirmation so we can ensure that the correct IP is allowlisted in Banco Carrefour's WAF and continue investigating the access blocks affecting our iOS automation executions.

Best regards,  
Felipe Milagres