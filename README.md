# AzureInfra

## Project Structure

- **linux-vm/**  
  Contains all Terraform code for deploying a Linux VM, including networking, security, and storage resources.
- **infra/bicep/**  
  Contains Bicep files for deploying Azure infrastructure as an alternative to Terraform.
- **aks/**
  Reference for creating the aks and deploying aks-store-quickstart application
  [AKS Application](https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application?tabs=azure-cli)


#### Features

- **Randomized Resource Group Name:** Ensures unique resource group names for each deployment.
- **Virtual Network & Subnet:** Isolated network environment for the VM.
- **Network Security Group:** Allows SSH (port 22) access; easily extendable for other rules.
- **Public IP Address:** Assigns a static public IP to the VM.
- **Storage Account:** Used for VM boot diagnostics.
- **SSH Key Authentication:** Secure login using SSH keys (no passwords).
- **Ubuntu 22.04 LTS:** Uses the latest Canonical Ubuntu Server image.
- **Parameterization:** Easily customize location, VM size, username, and more via variables.

#### Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) v1.0 or later
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- An Azure subscription
- SSH key pair (public key)

#### Usage

1. **Clone the repository:**
    ```sh
    git clone https://github.com/<your-username>/<your-repo>.git
    cd <your-repo>/linux-vm
    ```

2. **Authenticate with Azure:**
    ```sh
    az login
    ```

3. **Initialize Terraform:**
    ```sh
    terraform init
    ```

4. **Customize variables (optional):**
    - Edit `variables.tf` or use a `terraform.tfvars` file to override defaults (e.g., location, username, etc.).

5. **Apply the configuration:**
    ```sh
    terraform apply
    ```
    - Review the plan and type `yes` to confirm.

6. **Access your VM:**
    - Find the public IP in the Terraform output or Azure Portal.
    - SSH into the VM:
      ```sh
      ssh <username>@<public_ip>
      ```

#### Outputs

- **resource_group_name:** The name of the created resource group.
- **public_ip_address:** The public IP address of the Linux VM.

#### Clean Up

To destroy all resources created by this deployment:
```sh
terraform destroy
```

#### Notes

- The `.terraform/` directory and Terraform state files are **not** tracked in git.
- Never commit sensitive files or provider binaries to your repository.
- You can extend this configuration to support multiple environments by using [Terraform workspaces](https://www.terraform.io/docs/language/state/workspaces.html) or modules.

#### File Structure

```
linux-vm/
├── main.tf
├── variables.tf
├── output.tf
├── providers.tf
├── ssh.tf
├── .terraform.lock.hcl
├── terraform.tfstate (generated)
└── terraform.tfvars (optional)
```


**Author:** [Manupendra Tiwari]  
**Contact:** [manupendratiwari@gmail.com]
