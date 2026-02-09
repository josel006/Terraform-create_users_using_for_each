# Terraform-create_users_using_for_each

## Create AWS IAM users using the `for_each` meta-argument

This exercise demonstrates how to create **multiple AWS IAM users** using Terraform’s **`for_each`** meta-argument.

Unlike `count`, `for_each` allows you to **safely add or remove users in the future** without forcing Terraform to destroy and recreate existing resources. This makes it the preferred approach for managing IAM users over time.

---

## Why use `for_each` instead of `count`
With `for_each`:
- Each user is tracked by a **unique key**
- You can add or remove users without index shifting
- Existing users remain untouched unless explicitly removed

This makes `for_each` ideal for resources like IAM users that should not be recreated accidentally.

---

## Initial users list
The following screenshot shows the initial list of users defined in Terraform:

<img width="1182" height="315" alt="image" src="https://github.com/user-attachments/assets/c7c73ac4-2863-4518-9c4e-99599fc61c01" />

---

## Terraform execution
Run the following commands from your project directory:

```bash
terraform init
terraform validate
terraform plan
terraform apply -auto-approve

```

## Terraform execution
Validation in AWS Console

After applying the configuration, the IAM users can be validated in the AWS Console:

<img width="690" height="461" alt="image" src="https://github.com/user-attachments/assets/bab6e3fa-154e-4d42-ab52-7ddd955453fa" />
Updating the users list

One of the main advantages of for_each is the ability to edit the users list safely.

In this example, a new user named user100 was added in VS Code:

<img width="1138" height="83" alt="image" src="https://github.com/user-attachments/assets/624e81a7-761a-4a7c-a5b3-d742ed6d5d5e" />
Steps:

Save the changes in VS Code

```bash
terraform validate
terraform plan
terraform apply -auto-approve

```


Terraform will detect only the new user and create it without affecting existing users.

## Final validation

After applying the changes, the new user100 can be confirmed in the AWS Console:

<img width="715" height="499" alt="image" src="https://github.com/user-attachments/assets/631271d6-6c67-49d6-922a-0f499612df5c" />
Key takeaway

count is index-based and can cause unintended resource replacement

for_each is key-based and safer for long-term resource management

For IAM users and similar resources, for_each is the recommended approach
