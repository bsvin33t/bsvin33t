Here is the pull request template that we use during our application development(specific to github).
It lives inside the `.github` directory of the project.


``` markdown

### Issue link
[Link]()

### Summary
_(Summarize the issue in couple sentences so others could be on the same page during the review. **What** is being changed. **Why** are we doing this? **How** are we doing this?)_

### QA instructions
_(How this issue could be tested: test data, test env name etc.)_


### Deploy instructions
_(If applied: shall a rake task be running, any migrations to be applied?)_

🔥 Please consider SP-WEB during the deploy!

---

**😎 NOTE**: please remember to name your branch with proper namespace:
- `feature/something`
- `release/something`
- `hotfix/something`
etc.

**TODO**:
- [ ] write a succinct and self-explanatory title
- [ ] link to the Jira ticket
- [ ] summary
- [ ] QA instruction
- [ ] delete notes
- [ ] make sure you create a clean-up ticket for feature toggles, logging, etc and add comments around the call referencing the ticket (eg. TODO-PRCORE-XXXX where PRCORE-XXXX is the clean-up ticket)


```

