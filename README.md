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
1.	Docker exec [container_name] cat/var/jenkins_home/secrets/initialAdminPassword on your terminal to the get Jenkins password, paste it and press Continue.
2.	press install suggested plugins and wait for in to finish.
3.	Fill out your information and press save and continue.
4.	Check that the URL is correct and press continue.
5.	Press Start using Jenkins.
4. Making the connection:
1.	Press on "Manage Jenkins" and then press on "Plugins".
2.	Press on "Available plugins", then type in "JIRA Pipeline Steps" and install it.
3.	Go back to the manage Jenkins window and press on Credentials.
4.	Press on "(global)" and then press on "Add Credentials".
5.	Leave the type as "Username and Password" and fill them up as well as the ID and Description, and press create.
6.	Go back to the manage Jenkins window and press on system.
7.	Scroll down until you find the "JIRA Steps" part and press "Add Site".
8.	Write Jira as the name and http://jira:8080 as the URL.
9.	Choose Credentials as the login type, and select the credenitals you entered earlier.
10.	 Press on "Test Connection" and verify it returns "Success".
<div align="center"><img src="/Images/site.png" alt="site" width="780" height="398"></div>

11.	 Scroll up and find the "Global properties" and check the “Environment variables” box and press add.
12.	 Fill out "JIRA_SITE" as the name and the site name you chose earlier, in this case Jira, as the value.
<div align="center"><img src="/Images/var.png" alt="var" width="785" height="162"></div>

13.	 Press save and you’re Done!


### Testing:
1.	Create a new Jira project.
2.	Create an issue in the project.
3.	Check the Transition ID for the transition between To do and Done.
4.	Create a Jenkins pipeline and call it by the issue key:
<div align="center"><img src="/Images/1.png" alt="site" width="230" height="73"><img src="/Images/2.png" alt="site" width="242" height="73"></div>

5.	Copy the contents of the Jenkinsfile file and change the id to your project's TransitionID.
6.	Press save, and then press on Build Now.
7.	Check that the build was successful, if so, continue to the next step.
8.	Refresh the Jira page and confirm the issue switched to "Done".



## Research and Preparation:
### benefits of integrating Jenkins and Jira:
-	Allows you to have automated issue updates based on build status.
-	Reduces the manual work.
-	Eliminates the chances of human error and unnecessary builds.
-	Helps the Jira and the team members to be up to date on what builds were done successfully without checking it in Jenkins.
-	Allows you to have a clear understanding of what’s next on the agenda with limited efforts.
