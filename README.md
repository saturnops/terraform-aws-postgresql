# Terraform Module for AWS RDS PostgreSQL


<br>
This Terraform module deploys a PostgreSQL database on AWS RDS, simplifying the setup and management of cloud-based relational databases.



## Usage Examples
```hcl
module "rds-pg" {
  source                           = "saturnops/postgresql-rds/aws"
  name                             = "postgresql"
  db_name                          = "proddb"
  vpc_id                           = "vpc-047eb8acfb73"
  multi_az                         = "true"
  subnet_ids                       = ["subnet-b39cfc", "subnet-090b8d8"]
  environment                      = "prod"
  kms_key_arn                      = "arn:aws:kms:region:2222222222:key/f8c8d802-a34b"
  engine_version                   = "15.2"
  instance_class                   = "db.m5.large"
  master_username                  = "pguser"
  allocated_storage                = "20"
  publicly_accessible              = false
  skip_final_snapshot              = true
  backup_window                    = "03:00-06:00"
  maintenance_window               = "Mon:00:00-Mon:03:00"
  major_engine_version             = "15.2"
  deletion_protection              = false
  allowed_security_groups          = ["sg-013cbf880"]
  final_snapshot_identifier_prefix = "final"
}
```
Refer [examples](https://github.com/saturnops/terraform-aws-rds-postgresql/tree/main/example/complete) for more details.

## IAM Permissions
The required IAM permissions to create resources from this module can be found [here](https://github.com/saturnops/terraform-aws-rds-postgresql/blob/main/IAM.md)

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | 3.43.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | 3.43.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_db"></a> [db](#module\_db) | terraform-aws-modules/rds/aws | ~> 3.0 |
| <a name="module_security_group_rds"></a> [security\_group\_rds](#module\_security\_group\_rds) | terraform-aws-modules/security-group/aws | ~> 4 |

## Resources

| Name | Type |
|------|------|
| [aws_security_group_rule.cidr_ingress](https://registry.terraform.io/providers/hashicorp/aws/3.43.0/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.default_ingress](https://registry.terraform.io/providers/hashicorp/aws/3.43.0/docs/resources/security_group_rule) | resource |
| [aws_availability_zones.available](https://registry.terraform.io/providers/hashicorp/aws/3.43.0/docs/data-sources/availability_zones) | data source |
| [aws_region.current](https://registry.terraform.io/providers/hashicorp/aws/3.43.0/docs/data-sources/region) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_additional_tags"></a> [additional\_tags](#input\_additional\_tags) | A map of additional tags to apply to the AWS resources | `map(string)` | <pre>{<br>  "automation": "true"<br>}</pre> | no |
| <a name="input_allocated_storage"></a> [allocated\_storage](#input\_allocated\_storage) | The allocated storage capacity for the database in gibibytes (GiB) | `number` | `20` | no |
| <a name="input_allowed_cidr_blocks"></a> [allowed\_cidr\_blocks](#input\_allowed\_cidr\_blocks) | A list of CIDR blocks that are allowed to access the database | `list(any)` | `[]` | no |
| <a name="input_allowed_security_groups"></a> [allowed\_security\_groups](#input\_allowed\_security\_groups) | A list of Security Group IDs to allow access to the database | `list(any)` | `[]` | no |
| <a name="input_apply_immediately"></a> [apply\_immediately](#input\_apply\_immediately) | Specifies whether any cluster modifications are applied immediately or during the next maintenance window | `bool` | `false` | no |
| <a name="input_backup_retention_period"></a> [backup\_retention\_period](#input\_backup\_retention\_period) | The number of days to retain backups for | `number` | `5` | no |
| <a name="input_backup_window"></a> [backup\_window](#input\_backup\_window) | The preferred window for taking automated backups of the database | `string` | `""` | no |
| <a name="input_create_random_password"></a> [create\_random\_password](#input\_create\_random\_password) | Whether to create a random password for the RDS primary cluster | `bool` | `true` | no |
| <a name="input_create_security_group"></a> [create\_security\_group](#input\_create\_security\_group) | Whether to create a security group for the database | `bool` | `true` | no |
| <a name="input_db_name"></a> [db\_name](#input\_db\_name) | The name of the automatically created database on cluster creation | `string` | `""` | no |
| <a name="input_deletion_protection"></a> [deletion\_protection](#input\_deletion\_protection) | Specifies whether accidental deletion protection is enabled | `bool` | `true` | no |
| <a name="input_enable_ssl_connection"></a> [enable\_ssl\_connection](#input\_enable\_ssl\_connection) | Whether to enable SSL connection to the database | `bool` | `false` | no |
| <a name="input_engine"></a> [engine](#input\_engine) | The name of the database engine to be used for this DB cluster | `string` | `"postgres"` | no |
| <a name="input_engine_version"></a> [engine\_version](#input\_engine\_version) | The database engine version. Updating this argument results in an outage | `string` | `""` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Select enviroment type: dev, demo, prod | `string` | `""` | no |
| <a name="input_family"></a> [family](#input\_family) | The version of the Postgresql DB family being created | `string` | `"postgres15"` | no |
| <a name="input_final_snapshot_identifier_prefix"></a> [final\_snapshot\_identifier\_prefix](#input\_final\_snapshot\_identifier\_prefix) | The prefix name for the final snapshot on cluster destroy | `string` | `"final"` | no |
| <a name="input_instance_class"></a> [instance\_class](#input\_instance\_class) | The instance type for the database | `string` | `"db.m5.large"` | no |
| <a name="input_kms_key_arn"></a> [kms\_key\_arn](#input\_kms\_key\_arn) | The ARN for the KMS encryption key. Set this to the destination KMS ARN when creating an encrypted replica. If storage\_encrypted is set to true and kms\_key\_id is not specified, the default KMS key created in your account will be used | `string` | `null` | no |
| <a name="input_maintenance_window"></a> [maintenance\_window](#input\_maintenance\_window) | The preferred window for performing database maintenance | `string` | `""` | no |
| <a name="input_major_engine_version"></a> [major\_engine\_version](#input\_major\_engine\_version) | The major engine version for the database. Updating this argument results in an outage | `string` | `""` | no |
| <a name="input_master_username"></a> [master\_username](#input\_master\_username) | The username for the RDS primary cluster | `string` | `""` | no |
| <a name="input_multi_az"></a> [multi\_az](#input\_multi\_az) | Enable multi-AZ for disaster recovery | `bool` | `false` | no |
| <a name="input_name"></a> [name](#input\_name) | The name of the RDS instance | `string` | `""` | no |
| <a name="input_port"></a> [port](#input\_port) | The port number for the database | `number` | `5432` | no |
| <a name="input_publicly_accessible"></a> [publicly\_accessible](#input\_publicly\_accessible) | Specifies whether the RDS instance is publicly accessible over the internet | `bool` | `false` | no |
| <a name="input_random_password_length"></a> [random\_password\_length](#input\_random\_password\_length) | The length of the randomly generated password for the RDS primary cluster (default: 10) | `number` | `10` | no |
| <a name="input_replicate_source_db"></a> [replicate\_source\_db](#input\_replicate\_source\_db) | Specifies that this resource is a replicate database, and uses the specified value as the source database identifier | `string` | `null` | no |
| <a name="input_skip_final_snapshot"></a> [skip\_final\_snapshot](#input\_skip\_final\_snapshot) | Determines whether a final DB snapshot is created before the DB instance is deleted. If set to true, no DB snapshot is created. If set to false, a DB snapshot is created before the DB instance is deleted, using the value from final\_snapshot\_identifier | `bool` | `true` | no |
| <a name="input_snapshot_identifier"></a> [snapshot\_identifier](#input\_snapshot\_identifier) | Specifies whether to create the database from a snapshot. Use the snapshot ID found in the RDS console, e.g., rds:production-2015-06-26-06-05 | `string` | `null` | no |
| <a name="input_storage_encrypted"></a> [storage\_encrypted](#input\_storage\_encrypted) | Specifies whether to enable database encryption | `bool` | `true` | no |
| <a name="input_subnet_ids"></a> [subnet\_ids](#input\_subnet\_ids) | A list of subnet IDs used by the database subnet group | `list(any)` | `[]` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | The ID of the VPC where the RDS cluster will be deployed | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_db_instance_endpoint"></a> [db\_instance\_endpoint](#output\_db\_instance\_endpoint) | Connection endpoint of the RDS instance. |
| <a name="output_db_instance_name"></a> [db\_instance\_name](#output\_db\_instance\_name) | Name of the database instance |
| <a name="output_db_instance_password"></a> [db\_instance\_password](#output\_db\_instance\_password) | Password for accessing the database (Note: Terraform does not track this password after initial creation). |
| <a name="output_db_instance_username"></a> [db\_instance\_username](#output\_db\_instance\_username) | Master username for accessing the database. |
| <a name="output_db_parameter_group_id"></a> [db\_parameter\_group\_id](#output\_db\_parameter\_group\_id) | ID of the parameter group associated with the RDS instance. |
| <a name="output_db_subnet_group_id"></a> [db\_subnet\_group\_id](#output\_db\_subnet\_group\_id) | ID of the subnet group associated with the RDS instance. |
| <a name="output_rds_dedicated_security_group"></a> [rds\_dedicated\_security\_group](#output\_rds\_dedicated\_security\_group) | ID of the security group associated with the RDS instance. |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->






##           





Please give our GitHub repository a ⭐️ to show your support and increase its visibility.





