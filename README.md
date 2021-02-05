# codecommit-merge-request-approval-pipeline

CodeCommit merge and pull requests trigger an event in AWS that can be captured and used to automatically notifiy approvers that a pull request occured, allowing them to click a link to approve it. This sample
is just a simple template of how to create a function that responds to this event, creates a message that includes an API gateway url for the approver to click, which triggres a second function to actually do the merge.

SAM templates are used to simply create lambda functions and tie a trigger to them without writing too much code. In our example, the deployment template creates a 2 lambda functions, one which is triggered by
a codecomit pull-request state change and the other is trigger by an API gateway GET using query parameters as the pull-request ID. 

NOTE: Due to limited documentation out there, manual steps are required for deployment. Currently, the first function in the pipeline that is triggered by codecommit must have the API gateway URL set in it's environment
variable. You cannot simply '!Ref' this in a SAM template as the API is created implicitly. Thus, after deploying this template, you must edit the MergeAlert function to include the API gateway URL that was created by the
second function. 