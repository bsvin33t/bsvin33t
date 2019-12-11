Since we have some problems with the current approach that we used, as a team we decided on changing our git process to use git-flow with some small adjustments to our needs.
See git-flow explanation

profis git-flow
Basically, we will have two main branches, develop and master in our repository.

Master always contains the production code that is currently running. Whenever we need to rollback production deployment or revert something from running production code, they need to be reflected on the master branch. It’s important since we don’t want to confuse with having different code bases on production instances and master branch.

Develop branch is the base branch of new features. When you want to start to work on a new feature, it should be based on the develop branch. After code review, you can use preview environments and QA the ticket and then you can merge your feature branch into the develop. The convention for the feature branch name is feature + jira ticket number + small description, like feature/PRCORE-500-add-document-uploader





core-api flow
When we merge feature branches to develop branch, it’s going to be automatically deploy develop to check24-test environment.

When we want to deploy to production, we need to create a new release branch from the current develop branch and trigger the production deployment with the release branch through charlie bot. After successfully deploying the release branch we finish it by merging it to the master and master to develop.
(Trying to automate this with charlie-bot to get more transparency)

For the hotfixes that we need, we will create a release hotfix branch and merge it to master. And then we also need to create another PR to apply the same hotfix to develop branch.

To be able to use gitflow, you can use both raw git commands or git-flow commands. To see the comparison of the commands you can check this gist.




Deploy to production
We will use charliebot to deploy our branches:
To deploy sp-admin to production we would run the following commands:

deploy the release branch to production:
charlie deploy sp-admin/release/20190322-1 to production

After deployment
Monitor sentry and the system load to figure out if a deployment introduced problems for some time (min. 10 Minutes)
on errors: which might be introduced by the deployment, rollback the migrations and deploy the master manually from jenkins.
on success: finish the release as described above

Commands to run
When building a feature
git checkout develop
git checkout feature/ticket_number_ticket_title

When Fixing a bug
git checkout develop
git checkout bug/ticket_number_ticket_title

When done with the feature or bug
git push origin branch_name

Open a pull request with develop branch as base. Once approved, merge it to develop branch.

When deploying to production
git checkout develop

git pull origin develop
git checkout -b release/$(date +%Y%m%d)-1

git push origin release/$(date +%Y%m%d)-1

At this point, the release branch is ready to be deployed, release tag can be created.
run profibot deploy core-api/release/20190322-1 to production

Alternatively you can use the following command for profibot in slack directly.
deploy core-api/release/20190322-1 to production

Deploy release branch to production

Head to Jenkins, choose "Build with Parameters", enter release branch name, click "Build"

monitor the deployment 10 to 15 mins

if there are no errors

git checkout master

git pull --rebase

git merge origin release/$(date +%Y%m%d)-1

git push origin master

git tag -a $(date +%Y%m%d)-1 -m $(date +%Y%m%d)-1

git push origin $(date +%Y%m%d)-1

git checkout develop

git merge master

git push origin develop

If there are errors
run profibot deploy master

Release master branch.

How to do a hotfix
git checkout master 
git checkout -b hotfix/$(date +%Y%m%d)-1
Do your fix and commit on the hotfix/$(date +%Y%m%d)-1 branch
git push origin hotfix/$(date +%Y%m%d)-1

At this point, the hotfix is ready to be deployed
run charlie deploy sp-admin/hotfix/20190322-1 to production

monitor the deployments 10 to 15 mins

if there are errors
run charlie deploy master

if there are no errors
git checkout master
git merge hotfix/yyyyddmm-1
git push origin master
git checkout develop
git merge master
git push origin develop

Special scenario, where you have already merged the release branch and later you see that there are errors
git checkout master

git revert tagname(might cause merge conflicts)

git push origin master

run charlie deploy master

Note: When doing the last step, you might be needed to open a PR to merge master to develop and this will contain only the merge commits coming from the deployment branch. This is OK and expected.
We will approve the PRs once every month. If it is blocking you(it should not, but if it does, something must have gone wrong), grab your closest colleague(investigate if necessary) , and get them to approve this PR which contains only merge commits
        



