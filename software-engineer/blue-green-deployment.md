# Blue Green Deployment
Blue green deployments are often used for consumer-facing applications and applications with critical uptime requirements. New code is released to the inactive environment, where it is thoroughly tested. Once the code has been vetted, the team makes the idle environment active, typically by adjusting a router configuration to redirect application program traffic. The process reverses when the next software iteration is ready for release.

If problems are discovered after the switch, traffic can be directed back to the idle configuration that still runs the original version. Once the new code has proven itself in production, the team may choose to update code in the idle configuration environment to provide an added measure of capability for disaster recovery.
