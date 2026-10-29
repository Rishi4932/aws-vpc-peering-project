# AWS VPC Peering — EWB Student Project

## Project overview
This lab connects two Amazon VPCs using VPC peering and verifies private communication between EC2 instances. The bastion host in VPC A is used for administration; App-A and App-B remain private.

## Region
Asia Pacific (Sydney): `ap-southeast-2`

## Actual configuration recorded during the lab
| Resource | CIDR / private IP |
|---|---|
| `ewb-vpc-a` | `10.10.0.0/16` |
| `ewb-a-public` | `10.10.1.0/24` |
| `ewb-a-private` | `10.10.2.0/24` |
| `ewb-vpc-b` | `10.20.0.0/16` |
| `ewb-b-private` | `10.20.1.0/24` |
| `ewb-bastion` | `10.10.1.153` |
| `ewb-app-a` | `10.10.2.219` |
| `ewb-app-b` | `10.20.1.108` |
| Peering | `ewb-a-b-peer` — Active (last confirmed) |

> These are the actual IPs reported during the lab, not the example IPs in the workbook. Recheck current AWS details before submission. Record resource IDs in the final PDF.

## Route table summary
- `ewb-rt-a-public` (associated with `ewb-a-public`): local VPC A route; `0.0.0.0/0` to `ewb-igw-a`; `10.20.0.0/16` to `ewb-a-b-peer`.
- `ewb-rt-a-private` (associated with `ewb-a-private`): local VPC A route; `10.20.0.0/16` to `ewb-a-b-peer`.
- `ewb-rt-b-private` (associated with `ewb-b-private`): local VPC B route; `10.10.0.0/16` to `ewb-a-b-peer`.

## Verified tests reported so far
- Peering status: Active.
- Bastion SSH: successful.
- Bastion to App-A SSH: successful.
- App-A to App-B ping: 4 packets received, 0% packet loss.
- App-A to App-B SSH: successful.
- App-B hostname and private IP: verified.

## Still required by the EWB workbook
- Baseline failed ping before peering/routes (only include if you captured it).
- Reverse ping from App-B to App-A.
- Controlled ICMP failure and recovery evidence.
- Security group inbound-rule screenshots and actual resource IDs.
- Proof App-A and App-B have no public IPv4 address.
- Cleanup evidence and learning summary.
- Export the final report as `YourName_EWB_VPC_Peering.pdf`.

## Security
Never commit `.pem` files, AWS access keys, passwords, session tokens, or other secrets.
