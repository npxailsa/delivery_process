# delivery_process
Repo for all the integrations built into the delivery process

## Security

### Handling Credentials
**Never commit service account keys or other sensitive credentials to the repository.**

To provide credentials for local development or in production:
1. Use environment variables (e.g., `GOOGLE_APPLICATION_CREDENTIALS`).
2. Use Google Cloud Secret Manager to securely store and retrieve secrets.
3. For local development, you can use a service account key file. **Do not commit this file.** Use `process_interface/credentials.json.example` as a template to create your own `process_interface/credentials.json`.
4. Alternatively, use the [Google Cloud CLI](https://cloud.google.com/sdk/docs/install) to authenticate:
   ```bash
   gcloud auth application-default login
   ```

### Security Tooling
This repository uses `pre-commit` to ensure code health and prevent the accidental commitment of secrets.

To set up pre-commit hooks:
1. Install `pre-commit`: `pip install pre-commit`
2. Install the hooks: `pre-commit install`

The `detect-secrets` hook is used to scan for potential secrets in your changes.

### Rotating Compromised Keys
If a private key has been committed to the repository:
1. **Immediately revoke the key** in the Google Cloud Console.
2. Delete the key file from the repository.
3. Update the `.gitignore` file to prevent future accidental commits of sensitive files.
