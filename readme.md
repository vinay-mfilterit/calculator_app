CI/CD in a Team: Concepts & Scenarios
In a real company, you rarely work alone. You work in a team with other developers. This guide explains how CI/CD helps teams work together without breaking things.

Key Concepts
1. Branching Strategy 🌿
Instead of everyone pushing to main (which is dangerous!), teams use branches:

main (Production): This is the "Live" code. It must always work.
dev (Development/Staging): This is where everyone's code meets first. It's like a rehearsal.
feature/xxx (Feature Branches): Example: feature/login-page. This is your private workspace. You do your work here, break things, fix them, and only share when ready.
2. Pull Request (PR) 🔄
A PR is a request to merge your feature branch into dev or main.

It's a "checkpoint".
Code Review: Peers read your code to find bugs.
Automated Checks: CI runs tests automatically on your PR. If tests fail, you cannot merge.
3. Continuous Integration (CI) 🤖
CI happens before code is merged.

Scenario: You delete a function in your feature branch.
Action: You open a PR.
CI System: Runs all tests. Sees that other parts of the app rely on that function.
Result: ❌ fail. You are blocked from merging. You fix it, push again, CI passes ✅, then you merge.
4. Continuous Deployment (CD) 🚀
CD changes based on the branch:

On dev branch: Deploys to a Staging Server (internal testing).
On main branch: Deploys to Production Server (real users).
Example Scenarios
Scenario A: The Happy Path 🟢
Dev creates feature/add-multiply.
Dev implements 
multiply()
 and adds tests.
Dev pushes and opens PR to dev.
CI runs tests. Result: ✅ Pass.
Team Lead reviews code. Result: "Looks good!"
Merge! code goes to dev.
CD automatically deploys dev to Staging.
QA team tests it manually. PASS.
PR opened from dev to main. Merge.
CD automatically deploys to Production.
Scenario B: The "Oops" Moment 🔴
Dev creates feature/refactor-math.
Dev changes how 
add()
 works but forgets to update tests.
Dev pushes and opens PR.
CI runs tests. Result: ❌ Fail.
GitHub blocks the merge button. 🚫
Dev sees the error, fixes the test locally, pushes again.
CI runs again. Result: ✅ Pass.
Now it's safe to merge.