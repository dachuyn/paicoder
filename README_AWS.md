# pAiCoder — AWS Deployment

pAiCoder can take a system diagram or description, generate a complete
AWS deployment (CloudFormation stack, deployment scripts, .env, configs.py, etc), and deploy the solution to AWS cloud for you! 

## Quick Start

  1. Open your project in VS Code with pAiCoder installed
  2. Cmd+Shift+P → pAiCoder: Setup - Configure API Keys & Roles
  3. Add a design diagram or description file 
  4. Right-click -> "Load-Design from this file"
  5. Or from pAiCoder CHAT panel, type "load-design path/to/filename"
  6. Or from pAiCoder CHAT panel, type "design text-description "
  7. Fill in required secrets/keys and run "aws-deploy"

## What Gets Generated 

  aws/

    cloud/

      stack.yaml          CloudFormation template

      parameters.json     Stack parameters

      README.md           Deployment instructions

      deploy.sh           Local deploy script

  .env                    secrets, keys, etc

  configs.py              configurable settings

## Contact

  GitHub:  https://github.com/dachuyn/paicoder
  Email:   supports@paicoder.com
