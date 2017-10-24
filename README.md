# Bot Milestone

## Use Case Refinement
Based on our feedback we change the architecture and usecases descriptions. Our use cases are changed as follow:

Use Cases
---
```

Use Case 1: Provision a new Virtual Machine.
1. Preconditions
The user shall have AWS/Digital Ocean account with valid access keys. User shall also have valid Slack API token on their system

2. Main Flow:
User requests AutoBot to provision a new Virtual Machine [S1]. AutoBot asks about flavor of the requested machine [S2]. User selects the flavor of the VM [S3] AutoBot asks about configuration parameters [S4]. User provides configuration parameters [S5]. AutoBot creates a VM with provided parameters [S6]. 

3. SubFlows
   [S1] User requests the bot to provision a new Virtual Machine.
   [S2] The AutoBot shows different kinds of VMs to the user to select one of them. (plain   or flavored VM)
   [S3] The user selects one of the provided kind of VM.
   [S4] The AutoBot asks different configuration parameters from the user.
   [S5] The user provides configuration parameters.
   [S6] The AutoBot configured a VM based on the user selections and returns the configuration details of the created VM including access link, and credentials

4. Alternative Flows
   [E1] The AutoBot can not create a new VM based on some errors and return the failure message to the user. - error like the user has reached limit of VM’s he can create.

````
````
  
Use Case 2: Setup virtual machine with Eclipse and selective plugins installed using Packer.
1. Preconditions
User shall have valid Slack API token on their system, and eclipse installed in the environment.

2. Main Flow
User requests the AutoBot for a VM image with Eclipse pre-configured[S1]. AutoBot ask user whether or not to install any specific plugins on the configured eclipse[S2]. The user provides plugins to be installed[S3]. The AutoBot build VM image with eclipse and plugins configured using packer Io and gives the image back to user[S4].

3. Subflows : to be edited
   [S1] User requests the AutoBot to setup a local Eclipse workspace.
   [S2] AutoBot ask the user about the location of eclipse directory on the system.
   [S3] User provide the location of the Eclipse Directory.
   [S4] The AutoBot provides the list of available plugins and ask the user the select some of them. 
   [S5] The user selects desired plugins from the provided list.
   [S6] The AutoBot setups Eclipse workspace with selected plugins installed.

4. Alternative Flows
   [E1] User wants plugins that do not exist in the list of plugins which bot can install.
   [E2] AutoBot was not able to install the desired plugins, because of some errors: like internet issue/ download error.

````
````

Use Case 3: Management of Virtual Machines. 
1. Preconditions
The user shall have AWS/Digital Ocean account with valid access keys. User shall also have valid  Slack API token on their system. User shall have access to email service to read the OTP sent.

2. Main Flow
User says AutoBot that he wants to manage his VMs[S1]. The AutoBot shows all user’s reserved VMs [S2]. The user selects a specific VM [S3] The AutoBot asks user about desired action on selected VM: delete or configuration change [S4]. The user provides the choice [S5]. The AutoBot ask required parameters if needed [S6]. The user provides needed parameters [S7].The Autobot request confirmation from the user (OTP via email) [S8]. The user confirms the request [S9]. The Autobot changed the selected VM [S10].

3. Subflows
   [S1] User requests the AutoBot to manage VMs.
   [S2] The AutoBot lists all user’s reserved VMs.
   [S3] User selects a specific VM to change.
   [S4] AutoBot ask user to select a specific action for the selected VM: delete or change configuration
   [S5] The user selects one option. It can be one of the configuration change or tear down the machine. 
   [S6] The AutoBot asks required parameter of that configuration. (if needed. For example to tear down the VM no parameter is needed)
   [S7] The user enters different parameters (if needed).
   [S8] The Autobot request for providing OTP as a confirmation to change the VM. 
   [S9] The user confirms the request by providing valid OTP.
   [S10] The AutoBot changes the configuration of the selected VM based on given parameters or tears down it.

4. Alternative Flows
   [E1] The AutoBot is not able to configure the VM based on errors it may encounter and returns the failure message to the user.
   [E2] The user has no reserved VMs.
   [E3] The AutoBot is not able to delete the VM based on some errors and returns the failure message to the user.
   [E4] The user does not want to delete the VM after entering the main flow and request to go back to main menu.
   [E5] The user provided incorrect OTP, retry again with the OTP in his/her email.
   [E6] AutoBot locks delete Action for the user, after three incorrect attempts. AutoBot unlocks the delete action, after 10 minutes. 

````
## Mocking Service Component

We use "nock" to mock our api calls. In the following table you can see api calls that are mocked. The mock data files are located in /.

| Action   | api  
| ------------- | ------------ 
| Create a new vm     | POST /v2/droplets         
| Get IP of a vm      | GET /v2/droplets/:<dropletId>
| Delete a vm         | DELETE /v2/droplets/:<dropletId>

##### Week 1

| Deliverable   | Item/Status   |  Issues/Tasks
| ------------- | ------------  |  ------------
| Use Case Refinement      | Completed         |[TC1](https://trello.com/c/Y0Lggpq0)
| Bot Integration      | Completed             |[TC2](https://trello.com/c/ioz5nZQC)

##### Week 2

| Deliverable   | Item/Status   |  Issues/Tasks
| ------------- | ------------  |  ------------
| Bot Platform - Use Case 1     | In Progress        |[TC3](https://trello.com/c/UdeMZwB2) [PT1](https://www.pivotaltracker.com/story/show/152219898)
| Bot Platform - Use Case 2            |  In Progress        |[TC3](https://trello.com/c/UdeMZwB2) [PT2](https://www.pivotaltracker.com/story/show/152221185)
| Mock Data - Use Case 1      | In Progress            |  [TC4](https://trello.com/c/wm2htHJN) [PT3](https://www.pivotaltracker.com/story/show/152219339)

##### Week 3

| Deliverable   | Item/Status   |  Issues/Tasks
| ------------- | ------------  |  ------------
| Bot Platform - Use Case 1     | Completed        |[TC3](https://trello.com/c/UdeMZwB2) [PT4](https://www.pivotaltracker.com/story/show/152219898)
| Bot Platform - Use Case 2            |  In Progress        |[TC3](https://trello.com/c/UdeMZwB2) [PT5](https://www.pivotaltracker.com/story/show/152221185)
| Bot Platform - Use Case 3            |  In Progress        |[TC3](https://trello.com/c/UdeMZwB2) 
| Mock Data - Use Case 1      | Completed           |  [TC4](https://trello.com/c/wm2htHJN) [PT6](https://www.pivotaltracker.com/story/show/152219339)
| Mock Data - Use Case 2      | In progress          |  [TC4](https://trello.com/c/wm2htHJN) 
| Mock Data - Use Case 3      | Completed           |  [TC4](https://trello.com/c/wm2htHJN) 
| Selenium testing - Use Case 1      | In Progress           |  [TC5](https://trello.com/c/hGyeTPnd)
| Selenium testing - Use Case 2      | In Progress           |  [TC5](https://trello.com/c/hGyeTPnd)
| Selenium testing - Use Case 3      | In Progress           |  [TC5](https://trello.com/c/hGyeTPnd)
| Screencast      | In Progress       | [TC6](https://trello.com/c/BSYHFry7)
