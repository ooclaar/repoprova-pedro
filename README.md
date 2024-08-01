# Obrigado pela oportunidade

eb init -p docker repoprovapedro us-west-1
eb init
eb create repoprovapedro

Tentei seguir algumas abordagens
Criei todo o codigo terraform, porém faltanvam permissoes

aws_iam_instance_profile.ecs_node: Creation complete after 2s [id=demo-ecs-node-profile20240801213340254100000002]
╷
│ Error: creating ECR Repository (repoprovapedro): operation error ECR: CreateRepository, https response error StatusCode: 400, RequestID: 0615f927-05c1-4e91-b7ec-82f80dccbbbf, api error AccessDeniedException: User: arn:aws:iam::363838752048:user/pedrohenrique is not authorized to perform: ecr:CreateRepository on resource: arn:aws:ecr:eu-west-1:363838752048:repository/repoprovapedro because no identity-based policy allows the ecr:CreateRepository action
│
│   with aws_ecr_repository.this,
│   on main.tf line 80, in resource "aws_ecr_repository" "this":
│   80: resource "aws_ecr_repository" "this" {
│
╵
╷
│ Error: creating ECS Cluster (repoprovapedro): operation error ECS: CreateCluster, https response error StatusCode: 400, RequestID: a66a58d3-379d-4183-bde6-9a928684ee84, api error AccessDeniedException: User: arn:aws:iam::363838752048:user/pedrohenrique is not authorized to perform: ecs:CreateCluster on resource: arn:aws:ecs:eu-west-1:363838752048:cluster/repoprovapedro because no identity-based policy allows the ecs:CreateCluster action     
│
│   with aws_ecs_cluster.main,
│   on main.tf line 192, in resource "aws_ecs_cluster" "main":
│  192: resource "aws_ecs_cluster" "main" {
│
╵
╷
│ Error: creating CloudWatch Logs Log Group (/ecs/repoprovapedro): operation error CloudWatch Logs: CreateLogGroup, https response error StatusCode: 400, RequestID: 728b5ce4-90a5-4853-b194-a4ad9c6310a2, api error AccessDeniedException: User: arn:aws:iam::363838752048:user/pedrohenrique is not authorized to perform: logs:CreateLogGroup on resource: arn:aws:logs:eu-west-1:363838752048:log-group:/ecs/repoprovapedro:log-stream: because no identity-based policy allows the logs:CreateLogGroup action
│
│   with aws_cloudwatch_log_group.this,
│   on main.tf line 324, in resource "aws_cloudwatch_log_group" "this":
│  324: resource "aws_cloudwatch_log_group" "this" {
│
╵
╷
│ Error: creating EC2 VPC: operation error EC2: CreateVpc, https response error StatusCode: 403, RequestID: b32b309f-b960-475a-aa4b-eb4ed1eb1a35, api error UnauthorizedOperation: You are not authorized to perform this operation. User: arn:aws:iam::363838752048:user/pedrohenrique is not authorized to perform: ec2:CreateVpc on resource: arn:aws:ec2:eu-west-1:363838752048:vpc/* because no identity-based policy allows the ec2:CreateVpc action. Encoded authorization failure message: 6u9wArxRF0-FbzZr5c8L93hViyybRrkiOv3Z_jwzRqDVt74AUfDyMYYEFNU1Zo3-3FpASoTFvPVuSeaGDvtW2ok0PDe5O9rxJikFdy6kByURUdBpT-MDFf90uFKSU9X5zx3bchnUQiL_Vf4sSeSXXDluGHYbILvlVpE74j-YJmBW4CBfGSG3Ov05RkekIKqkEZGOVCy1uz0sl1on3Hpw-8FKjGodFrrULI9-n4XYyihZxz9wLhPztnhJ66Gu6xPrDxyoN0QRsj4ZwEQO3ZcXxtUEoQaA13CCjhCWW6EFGI6nU3fvuE88n1zRhR6U_VQjKRiUbDdG7_UDgZvjBA8YGhRZ4z3B94xEMpHxac5fVw_Ok_jG0LpBp5mqzI2v0djwZ5PpYa-nZI5aJTkmVslEfD-Uo3BeDgbXyCBXxkoLFwhIQxfj-AXyxVp04VFIZ7Imv8lCMBalmYnCwhLqyoUtcFpDwvsMPGY39fYbRiwbcius-w96eLoN-wATuST0SVlzztJIDA
│
│   with module.vpc.aws_vpc.this[0],
│   on .terraform/modules/vpc/main.tf line 28, in resource "aws_vpc" "this":
│   28: resource "aws_vpc" "this" {
│
╵

Acima ^classica vpc-ecs-alb

Logo após isso tentei seguir a abordagem do github action, vi que o tempo nao iria dar e também não tinha permissoes para adicionar secrets nem configurar o oidc