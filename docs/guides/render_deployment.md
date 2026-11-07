# Render deployment

One Docker web service runs the built frontend and CPU PPO service. ROS/Gazebo
and GPU training are separate. The gateway listens on `0.0.0.0:$PORT`, accepts
Render's exact `RENDER_EXTERNAL_HOSTNAME`, and forwards only the bounded PPO API
to the private loopback backend. Local Windows/Quick Tunnel behavior is preserved.

The supervisor waits for verified policy readiness before opening the gateway;
backend failure stops the container rather than serving a silently broken policy.
Health check: `/api/ppo/health`. One instance preserves in-memory mission sessions.
No database or persistent disk is required. Restarts/deployments reset missions.

## Deployment prerequisites

Deployment requires authorized access to the private implementation and its container configuration. This showcase cannot be deployed as the application.

Configure the hosting provider's GitHub integration for the private repository, select an appropriate compute plan, and validate the deployment configuration before creating a service. Keep credentials in provider-managed secrets. The service URL must come from the actual deployment.

Account identifiers, billing details, credit balances, and account-specific provisioning commands are omitted from this public edition. This historical preparation does not establish that a service was deployed.

## Validation completed

- Three gateway HTTP integration tests passed, including Render hostname,
  same-origin writes, rejected foreign origins/hosts and existing limits.
- Real supervisor startup on isolated local ports loaded the verified 753664-step
  checkpoint. Public-host-style requests passed health, mission creation,
  actual inference and session deletion.
- Node syntax checks passed. A local Docker engine is unavailable, so the Linux
  image build still needs validation on Render before claiming deployment success.
