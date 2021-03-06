Pre-requisites:
---------------	
1. Build Automation(Maven, Gradel, Ant, etc)
2. Understanding of Centralised Code Repositories(Gitlab, Github, Bitbucket, etc)/Version control system(VCS)/Source Control Management(SCM).

What were they doing before CI/CD?
-------------------------------
1. GitLab code commit,
2. integrate,
3. pull the committed code,
4. build and
5. verify in the local system.
6. Deploy to STG/Testing.
7. Manual Testing.
8. Deployment in Production

What is Continuous Integereation?
---------------------------------
Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early.

Continuous Integration (CI) consists of “executing” the build process as frequently as possible (ideally whenever a code change is checked into the source code control repository) and “verifying” the correctness of the resulting product, in particular by unit tests.

What is Continuous Delivery?
----------------------------
Delivering software to production with manual intervention.

What is Continuous Deployment?
------------------------------
Delivering software to production in an automated method.

![alt text](cd-vs-cde.png)

Why CI/CD?
----------
1. CI/CD includes the full automation of all steps between code commit to production deployment, thus reducing time and repeatable human works.
2. Implementing CI/CD allows teams to focus on building code and removes the overhead and potential human error in manual, mundane steps. 
3. CI/CD also makes the process of deploying new code quicker and less risky. 
4. Deployments then happen more frequently and in smaller increments, helping teams become more agile, more productive and more confident in their running code.

![CICD pipeline](cicd-pipeline.png)

What tools should I use?
------------------------
Build Automation : Maven, Gradel, Ant, etc.<br>
Version Control  : Gitlab, Github, Bitbucket,etc.<br>
CI/CD            : Jenkins, Teamcity, TravisCI, CircleCI, Bamboo, GoCD, etc.<br>
Deployment       : Octopus Deploy

CI/CD Good Practice:
--------------------
1. Build process should be under ten minutes.
2. Notifying about Build results(success/failed/stuck).
3. Fixing broken builds before adding more code.
4. Use simple branching structures that can be easy to sort through to find the link needed.
5. Don't Use “hotfixes” to release branches.
6. Determine the failure cause and location before shutting off failing tests.
7. Continuously testing code as soon as it is entered into the shared repository.
8. Manual testing and manual builds can be used but it will seriously limit the number of bugs caught.
9. Writing meaningful tests that can be run against every build to know if anything from the new code affected previous builds.

Reference Links:
----------------
[Microsoft's what is devops](https://azure.microsoft.com/en-in/overview/what-is-devops/#practices) <br>
[Plutora's understanding ci/cd pipeline](https://www.plutora.com/blog/understanding-ci-cd-pipeline) <br>
[Agilealliance's Automated build](https://www.agilealliance.org/glossary/automated-build/)<br>
[katalon's ci cd cheat sheet](https://www.katalon.com/resources-center/blog/ci-cd-cheat-sheet/)<br>
(This page is created by AATHITH(myself) for my self-reference only.)
