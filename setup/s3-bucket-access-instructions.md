# S3 Bucket Access Instructions

## What We Need From You

To grant your AWS account write access to our S3 bucket, we need one piece of information:

**Your AWS Account ID** — a 12-digit number that uniquely identifies your AWS account (e.g., `123456789012`).

---

## How to Find Your AWS Account ID

**Option 1 – AWS Console**
1. Sign in to the [AWS Management Console](https://console.aws.amazon.com)
2. Click your account name or email in the top-right corner
3. Your **Account ID** is displayed in the dropdown

**Option 2 – AWS CLI**
```bash
aws sts get-caller-identity --query Account --output text
```

---

## What to Send Us

Reply with your **12-digit AWS Account ID** and we'll handle the rest. Once we've updated the bucket policy, we'll send you the **bucket name** and **AWS region** so you can start writing.

---

## Optional: Scope Access to a Specific IAM Role or User

If you'd prefer we restrict access to a specific IAM role or user within your account (rather than your entire account), send us that principal's ARN instead. It will look like one of these:

- **Role:** `arn:aws:iam::123456789012:role/YourRoleName`
- **User:** `arn:aws:iam::123456789012:user/YourUserName`

This is the more secure option and is recommended if you know which principal will be performing the writes.

---

## How Cross-Account Access Works

AWS uses a **dual-permission model** for cross-account S3 access:

1. **Our side:** We add your account (or specific principal) to our bucket policy, which opens the door for your account.
2. **Your side:** The IAM user or role making the requests must also have an IAM policy that explicitly allows the relevant S3 actions.

Neither side alone is sufficient — both permissions must be in place for access to work.

### Example Bucket Policy

Once you provide your Account ID, we'll add a policy similar to this:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowExternalAccountWrite",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:root"
      },
      "Action": [
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

> **Note:** The `:root` principal grants access to the entire account — any IAM user or role in your account can act on it, as long as their own IAM policy also permits it.

---

## Example IAM Policy (Your Side)

Your IAM user or role will need a policy like this attached:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::our-bucket-name/*"
    }
  ]
}
```

We'll provide the exact bucket name and ARN once access is configured.
