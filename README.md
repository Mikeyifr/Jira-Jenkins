## Research and Preparation:
### benefits of integrating Jenkins and Jira:
-	Allows you to have automated issue updates based on build status.
-	Reduces the manual work.
-	Eliminates the chances of human error and unnecessary builds.
-	Helps the team members to be up to date on what build results without checking it in Jenkins.
-	Allows you to have a clear understanding of what’s next on the agenda.
-   Allows you to trace what build is linked to what issue and route you to that build with a click of a button.


## A step-by-step guide on Jira-Jenkins Integration

### Setting up:
1. Run "docker compose up -d" on your terminal to run the docker-compose.
2. Connect to the containers on your browser:
    - http://localhost:8081 for the Jenkins container
    - http://localhost:8082 for the Jira container


### Jira setup: *every point is a different page by order*
1.	Choose "I’ll set it up myself" and then press next.
2.	Leave it on "Built in", press next and wait for the setup to be over.
3.	Don’t change anything, make sure the base URL is correct and press next.
4.	Press on the "generate a Jira trial license" and connect to Atlassian.
5.	On the generate page make sure the License type is "Jira Software", fill everything else and press on the "Generate License" button.
6.	On the Confirmation window press "Yes".
7.	We’re back in the forth window only now the License is filled, press next.
8.	Fill out your information and your desired username and password and press next.
9.	Check the later box on the "Set up email notifications" form and press next.
10.	 Choose your language of choice and press next.
11.	 Choose an avatar and press next.


### Jenkins setup: *switch the [container_name] with the Jenkins container name*
1.	Run - Docker exec [container_name] cat /var/jenkins_home/secrets/initialAdminPassword - on your terminal to the get Jenkins password,
    paste it and press Continue.
2.	press install suggested plugins and wait for in to finish.
3.	Fill out your information and press save and continue.
4.	Check that the URL is correct and press continue.
5.	Press Start using Jenkins.
6. Making the connection:
7.	Press on "Manage Jenkins" and then press on "Plugins".
8.	Press on "Available plugins", then type in and install the following plugins:
    -   Jira
    -   Any Build Step
    -   Flexible Publish
9.	Go back to the manage Jenkins window and press on Credentials.
10.	Press on "(global)" and then press on "Add Credentials".
11.	Leave the type as "Username and Password" and fill them up as well as the ID and Description, and press create.
12.	Go back to the manage Jenkins window and press on system.
13. Scroll down a-bit until you see the "Flexible publish" part and change the "Allowed build steps" to "Any build step".
    <div align="center"><img src="/Images/publish.png" alt="flexible publish"></div>
14.	Scroll down again until you find the "Jira" part and press "Add".
15.	Write http://jira:8080/ as the URL.
    <div align="center"><img src="/Images/URL.png" alt="Jira URL"></div>
16. Check the ""Update Relevant Jira Issues For All Build Results" box.
17.	Choose your Credentials in the Credentials drop-down box.
    <div align="center"><img src="/Images/checkbox&cred.png" alt="checkbox&cred"></div>
18. Leave everything else as the default.
19.	Press on "Validate Settings" and verify it returns "Success".
    <div align="center"><img src="/Images/save&validate.png" alt="checkbox&cred"></div>
20.	 Press save and you’re Done!


### Testing:
1.	Create a new Jira project.
2.	Create an issue in the project.
3.	Create a Jira board and add a sprint with issues to the board.
4.	Create a freestyle Jenkins project.
5.	Make sure that you have a Jira site at the start of the page that shows the Url.
6.  We're going to add two Post-build Action.
    -   Jira: Update relevant issues, change the "Issue selector" to Explicit and type your issue-key.
    <div align="center"><img src="/Images/comment.png" alt="Jira: Update relevant issues"></div>
    -   Flexible publish, on the "Run?" box choose "Current build status" and leave the Statuses on "Success"
        On the Flexible publish box under the action section press Add, and Choose "Jira: Progress issues by workflow action"
        in the JQL Query type issueKey="[your issue-key]" and in the Workflow Action type Done.
    <div align="center"><img src="/Images/together.png" alt="workflow"></div>
6.	Press save, and then press on Build Now.
7.	Check that the build was successful, if so, continue to the next step.
8.	Confirm the issue switched to "Done" and that a comment that says SUCCESS with a link was added to the issue.
Optional testing - build failure:
9.  Add an "Execute shell" build step and write gibberish.
10. Press save, and then press on Build Now.
11. Confirm that the build has failed, if so, continue to the next step.
12. Confirm the issue stayed in the "To Do" column and that a comment that says FAILURE with a link was added to the issue.



## Testing process and results Report:




## Challenges:
### *p: problem | s: solution*
1.  p: I did not know what is the best approach to take at first, so I started with creating a pipeline that moves the issue to the Done
    column but I was missing the comment.

    s: I decided to go with a freestyle project and add everything as post-build actions.
    
2.  p: Using the post-build actions went well at first, but when I tried to test it on a failed build, and the issue still moved.

    s: I searched and downloaded various pluging that I found on the internet and found the Flexible Publish plugin that I used to create a condition.

3.  p: The Flexible Publish plugin didnt show the step I needed.

    s: I searched for different ways to add the step, including a plugin other than the flexible publish plugin until I found out on StackOverflow that there is a plugin that gives other plugins the ability to use all the build steps, so I used the Any Build Step           plugin to make the Flexible Publish plugin have more options for the step including the step I needed.
