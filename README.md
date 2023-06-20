# github-aws-oidc
A simple test to assume an IAM role in an AWS account from a github action.

## Setup
* create an OIDC Identity Provider in AWS (see cfn [idp.cfn.yml](./idp.cfn.yml))
* create an IAM role which can be assumed from this Identity Provider
  - make sure to add a condition to scope down the privileges so that only a github action from a certain github repo or branch can assume the role, e.g.
    ```json
    "Condition": {
      "StringLike": {
          "token.actions.githubusercontent.com:sub": "repo:<ORG_NAME/USER_NAME>/<REPO_NAME>:*"
      }
    ```
  > **Warning**
  > 
  > Without a condition statement referencing the `sub` claim from GitHub's OIDC provider the role will be **accessible from every other GitHub Action**
* create a GitHub Action file, e.g. `.github/workflows/aws.yml` and include the [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials) action

