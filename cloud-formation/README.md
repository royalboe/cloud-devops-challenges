# Cloud Formation Script

## Description

This is a cloud formation script to automate the creation of Network Compute infrastrutures on AWS.
This folder contains two template files and two parameter files.

## Files

- [Network Template File](./altschool-network.yml) | This file conations the script to create a VPC with 2 availability zones each containing a private and public subnet. Each of the public subnets contains a NAT gateway. The VPC network will also be created with an Internet gateway so that it can communicate with the Internet. There are route tables and route rules created also. This stack, after created successfully, it output some global values such as the id of the VPCs and Subnets can can be used by another stack.

- [Compute Template File](./altschool-server.yml) | This file contains script to automate the creation of servers in the private subnets. The servers are created as part of an Autoscaling group with one instance in each of the private subnets. The instances can only cummunicate with the internet using the NAT gateway. A load balancer is created that takes requests from users and direct the requests to the private instances, other than this, the private instances are not exposed to receive requests directly from the internet. In this file, you have to state your ssh key to access your private instances. You also have to state the ami value of the instance you want to use.

- [Network Parameters File](./altschool-network-parameters.json) | This file contains the parameter variables for the network file. In this file, you have to state the cidr block you want the network to use. You also have to state for the subnets.

- [Compute Parameters File](./altschool-servers-parameters.json) | This file contains the parameter variables for the server file

- [Create Stack](./create.sh) | This file is a script to run the aws cloud formation command to create a stack. You run it in this manner `./create.sh stack-name template-file parameter-file`.

- [Update Stack](./update.sh) | This file is a script to run the aws cloud formation command to update a stack. You run it in this manner `./update.sh stack-name template-file parameter-file`.