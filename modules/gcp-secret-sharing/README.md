# GCP Shared Secrets Module

Welcome to the **GCP Shared Secrets** module challenge! In this task, you’ll create and manage Google Cloud Platform secrets so that multiple projects can securely access them. Below is a high-level outline of what we're looking for.

---

## Overview

- **Host Project**: A main project where secrets will be created and stored.
- **Additional Projects**: One or more secondary projects that need access to the secrets.
- **Secrets**: A list of secret names you’ll create in the host project.
- **Service Accounts (SA)**: Each additional project will have its own service account(s) to read the secrets.

The main objective is to ensure that each project’s service account can securely read the secrets in the host project.

---

## Note

You can safely assume the following in the context of this challenge:

- All projects are already present and part of the same organization, you would not need to create those
- All secret values would be added later on after this module sets up the secrets and access
- Inputs can be considered correct, you do not need to validate them in your module

---

## Inputs

At a minimum, your module should acept the following variables to execute:

- The host project id
- A list of projects that will be readin the secret in the host project
- A list of secret names to create within the host project
- A configured `google` provider 

If you find other inputs help to accomplish the required tasks or allow for increased functionality you are free to add them.

---

## Requirements

1. **Create Secrets**
   - In the host project, create all specified secrets.

2. **Create Service Accounts**
   - In each additional project, provision at least one service account.

3. **Grant Access**
   - Make sure the service accounts in the additional projects can read the secrets in the host project.

4. **Outputs**
   - At minimum, output the names of the service accounts created.
   - Feel free to output other relevant information that you find helpful.

---

## Bonus Ideas

- **Selective Sharing**: Implement a way to exclude certain secrets from being shared with all service accounts.
- **Name Prefix**: Allow a common prefix for all service accounts to maintain consistent naming conventions.
- **Workload Identity**: As we use Kubernetes quite extensively having workload identity allows us to easily source secrets. Using the service accounts you created map them to a Kubernetes service account and namespace to allow accessing the secrets.

---

## Usage

Below is a simplified example of how this module might be used. Adjust as needed to fit your implementation:

```hcl
module "shared_secrets" {
  source             = "./path/to/your/module"
  host_project_id    = "my-host-project"
  project_ids        = ["my-project-one", "my-project-two"]
  secret_names       = ["db_password", "api_key", "payment_token"]
  service_account_prefix = "shared-secrets-sa"
  # Additional variables as needed ...
}
