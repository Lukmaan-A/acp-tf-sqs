Module usage:

     module "sqs" {
       source               = "git::https://github.com/UKHomeOffice/acp-tf-sqs?ref=master"
       name                 = "new-sqs"
       environment          = "env"
       sqs_iam_user         = "new-sqs-user"
       iam_user_policy_name = "new-sqs-policy"

       policy = <<POLICY
     {
       "Version": "2012-10-17",
       "Id": "sqspolicy",
       "Statement": [
         {
           "Sid": "First",
           "Effect": "Allow",
           "Principal": "*",
           "Action": "sqs:SendMessage",
           "Resource": "arn:aws:sqs:*:*:new-sqs",
           "Condition": {
             "ArnEquals": {
               "aws:SourceArn": "arn:aws:sqs:*:*:new-sqs"
             }
           }
         }
       ]
     }
     POLICY
     }


## Inputs

| Name | Description | Default | Required |
|------|-------------|:-----:|:-----:|
| content_based_deduplication | Enables content-based deduplication for FIFO queues | `false` | no |
| delay_seconds | The time in seconds that the delivery of all messages in the queue will be delayed. An integer from 0 to 900 (15 minutes) | `0` | no |
| environment | The environment the SQS is running in i.e. dev, prod etc | - | yes |
| fifo_queue | Boolean designating a FIFO queue | `false` | no |
| iam_user_policy_name | The policy name of attached to the user | - | yes |
| kms_alias | KMS key alias name for SQS | `` | no |
| max_message_size | The limit of how many bytes a message can contain before Amazon SQS rejects it. An integer from 1024 bytes (1 KiB) up to 262144 bytes (256 KiB) | `262144` | no |
| message_retention_seconds | The number of seconds Amazon SQS retains a message. Integer representing seconds, from 60 (1 minute) to 1209600 (14 days) | `345600` | no |
| name | A descriptive name for the SQS instance | - | yes |
| number_of_users | The number of user to generate credentials for | `1` | no |
| policy | The JSON policy for the SQS queue | `` | no |
| receive_wait_time_seconds | The time for which a ReceiveMessage call will wait for a message to arrive (long polling) before returning. An integer from 0 to 20 (seconds) | `0` | no |
| sqs_iam_user | The name of the iam user assigned to the created sqs bucket | - | yes |
| tags | A map of tags to add to all resources | `<map>` | no |
| visibility_timeout_seconds | The visibility timeout for the queue. An integer from 0 to 43200 (12 hours) | `30` | no |

