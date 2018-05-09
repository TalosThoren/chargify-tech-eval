# Description

A brief demonstration of basic Infrastructure-as-Code skills using AWS
CloudFormation templating.

## Problem statement

Write code-as-infrastructure script to launch a single EBS-backed EC2
instance. Include four additional EBS mounts of 10GB each. CLI,
CloudFormation, Terraform are all acceptable.

## Solution

The Ec2InstanceWithEbsVolumes.template file contains a simple CloudFormation
script that meets the requirements of the problem statement.

## Notes on implementation

Because this example is somewhat contrived, and because of time constraints, I
left out a great deal of what I might otherwise have liked to demonstrate.

For example, I would normally use a fairly standard ami region map for enforcing
the selection of certain sets of ami's for a template like this. I defaulted to
an Ubuntu 16.04 ami in an arbitrary region (us-west-2) for this example. The
default ami is a parameter and can be altered to any valid ami for any given
region.

I could have chosen multiple methods for creating and attaching the EBS volumes
to the instance, as well, and may not have chosen `DeviceBlockMapping` in a more
complex deployment.

I've not taken into account any VPC or subnetting here, and am allowing the
template to default to whatever subnet it wants in the default VPC. In
production scenarios, there would be quite a bit more work done on ensuring
template is portable between VPCs and Subnets within VPCs.

The template assumes the existence of an EC2 KeyPair, and requires the user to
provide one.

Creating appropriate security group rules is outside the scope of this template.

I would also typically include a Makefile or similar script for automated
launching of the template into an AWS environment. My preference is to upload
templates related to a deployment into a versioned S3 bucket, and use aws cli to
create stacks from the uploaded templates. This can be captured quite
effectively using GNU Make.
