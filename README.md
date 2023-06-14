# github-aws-oidc
A simple test to assume an IAM role in an AWS account from a github action.

## Setup
* create an OIDC Identity Provider in AWS (see cfn template)
* create an IAM role which can be assumed from this Identity Provider
  - make sure to add a condition to scope down the privileges so that only a github action from a certain github repo or branch can assume the role
* create a GitHub Action file
