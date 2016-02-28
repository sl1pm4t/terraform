---
layout: "remotestate"
page_title: "Remote State Backend: gcs"
sidebar_current: "docs-state-remote-gcs"
description: |-
  Terraform can store the state remotely, making it easier to version and work with in a team.
---

# gcs

Stores the state as a given key in a given bucket on [Google Cloud Storage](https://cloud.google.com/storage/).

-> **Note:** Passing credentials directly via config options will
make them included in cleartext inside the persisted state.
Use of environment variables or config file is recommended.

## Example Usage

```
terraform remote config \
	-backend=gcs \
	-backend-config="bucket=terraform-state-prod" \
	-backend-config="path=network/terraform.tfstate" \
	-backend-config="project=goopro"
```

## Example Referencing

```
resource "terraform_remote_state" "foo" {
	backend = "gcs"
	config {
		bucket = "terraform-state-prod"
		path = "network/terraform.tfstate"
		project = "goopro"
	}
}
```

## Configuration variables

The following configuration options / environment variables are supported:

 * `bucket` - (Required) The name of the GCS bucket
 * `path` - (Required) The path where to place/look for state file inside the bucket
 * `region` / `AWS_DEFAULT_REGION` - (Optional) The region of the S3 bucket
 * `endpoint` / `AWS_S3_ENDPOINT` - (Optional) A custom endpoint for the S3 API
 * `encrypt` - (Optional) Whether to enable [server side encryption](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)
    of the state file
 * `acl` - [Canned ACL](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl)
    to be applied to the state file.
 * `access_key` / `AWS_ACCESS_KEY_ID` - (Optional) AWS access key
 * `secret_key` / `AWS_SECRET_ACCESS_KEY` - (Optional) AWS secret key
 * `kms_key_id` - (Optional) The ARN of a KMS Key to use for encrypting the state.
