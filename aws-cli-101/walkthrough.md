# List all Regios

aws ec2 describe-regions --output table

# create a security group and open port 22

aws ec2 create-security-group --group-name example --description "this is an example"
aws ec2 authorize-security-group-ingress --group-name example --protocol tcp --port 22 --cidr 0.0.0.0/0

# create ec2 keypair

aws ec2 create-key-pair --key-name test-key --query 'KeyMaterial' --output text > test-key.pem

# get newest ami-linux image

aws ec2 describe-images --owners amazon --filters 'Name=name,Values=amzn2-ami-hvm-2.0.????????-x86_64-gp2' 'Name=state,Values=available' --output json | jq -r '.Images | sort_by(.CreationDate) | last(.[]).ImageId'

# describe all instance types

aws ec2 describe-instances

# run ec2 instance

aws ec2 run-instances --image-id ami-xxxxxxxx --security-group-ids xxxxxxxxx --instance-type t2.micro --key-name example-key

# get instance data

aws ec2 describe-instances --instance-ids i-0787e4282810ef9cf --query 'Reservations[0].Instances[0].PublicIpAddress'

# cleanup instances

aws ec2 stop-instances --instance-ids i-1234567890abcdef0
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0
