CircleCI YAML for RHMAP
=======================

For projects node.js Cloud Applications and MBaaS Services that wish to use
CircleCI for continuous integration and deployment this file can serve as a
starting point.

## CircleCI

CircleCI is a CI service that integrates with GitHub. If you are not using
GitHub for git hosting then you will need to use an alternative CI service.

## Running Tests on CircleCI
For node.js projects it is common convention that the _package.json_ contains
a "scripts" key that contains a "test" command. By default CircleCI will run
this command to perform tests. For an example you can check this [package.json](https://github.com/evanshortiss/rhmap-express-template/blob/master/package.json#L10).

## Anatomy of the circle.yml
For a full explanation of this file view the
[CircleCI Docs](https://circleci.com/docs/configuration/) on the subject.
We provide a basic overview of the file in this repo in the following sections.

### machine
Machine allows us to configure certain dependencies installed on our test
machine. We simply configure the machine to use node.js 0.10.33 since we want
to match the version used on RHMAP.

### dependencies
RHMAP uses an older version of MongoDB than is installed by default on the
CircleCI containers. We use the dependencies section to install the same
version that is running on RHMAP.

### deployment
Using this section enables you to add a deploy phase for builds. This will only
be triggered when a PR is merged, but not when it is opened - only the tests
will run when a PR is opened.

## Deployment to Red Hat Mobile
Deploying to Red Hat Mobile is achieved in the _deployment_ section as
mentioned above. This is a sample deploy script that will automatically deploy
to the "dev" environment on RHMAP whenever a PR is merged to the "dev" branch
on GitHub.

The variables required to run this script are as follows:

* FH_DOMAIN - The RHMAP instance, e.g mydomain.feedhenry.com
* FH_USER - The FHC user with deploy permissions, e.g deploys@myhost.com
* FH_PASS - The password for the FH_USER
* FH_GIT_URL - The Git URL from the Details screen of the Cloud Application or
Service
* FH_CLOUD_APP_ID - The AppID from the Details screen of the Cloud Application or
Service

Read [this post](http://developers.redhat.com/blog/2016/04/12/continuous-integration-and-deployment-for-red-hat-mobile-cloud-applications-using-circle-ci/) for more information on using CircleCI with RHMAP
