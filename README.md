# action-repo

**Purpose:**  
This repository is solely used to generate GitHub webhook events (Push, Pull Request, Merge). No application code lives here. Whenever someone pushes commits, opens a PR, or merges a PR, GitHub will send a JSON payload to our webhook endpoint.

## Webhook Configuration

1. Go to **Settings → Webhooks** in this repository.  
2. Click **Add webhook**.  
   - **Payload URL**: `https://<YOUR_FLASK_APP_DOMAIN>/github-webhook`  
   - **Content type**: `application/json`  
   - **Secret** (optional, but recommended): pick a secret string (e.g. `my_super_secret`).  
   - **Which events would you like to trigger this webhook?**  
     - Select **Let me select individual events**.  
     - Check **Push**, **Pull requests**, and **Pull request reviews** (the latter is not strictly needed, but Pull Requests themselves fire events).  
   - Click **Add webhook**.

Now, whenever you push commits or create/merge a PR, GitHub will POST JSON to our Flask receiver.

> **Note:** We assume your Flask app (in `webhook-repo`) is already deployed and publicly reachable at `https://<YOUR_FLASK_APP_DOMAIN>`. If you’re developing locally, use a tunneling tool (e.g. `ngrok`) and set the Payload URL accordingly (e.g. `https://<RANDOM>.ngrok.io/github-webhook`).
