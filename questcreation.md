# Quests Creation

### Terminology

- **Quest:** A series of steps, all connected together based on their topic.
- **Step:** A small task inside a quest. Usually, a step will represent a single user interaction.
- **Trigger:** An event in the system caused by the user. e.g., New chat message, PR opened, env var added to Heroku, etc.
- **Action:** A reaction to a triggered event that causes the user’s state in the quest to change. e.g., advance to next step, approve/reject user’s PR, send a message from bot, etc.
- **Conditions:** A way to check the user’s state. The state can be the text user entered in the chat, any piece of information attached to the trigger (e.g., PR Status), or information from a 3rd party service (e.g., env var value in Heroku)
- **FlowNode:** when a step starts or triggers are recognized, a Flow will begin. A single element in the flow is called FlowNode. A node is a combination of actions and conditions.
- **GitHub Actions:** command executed as part of GitHub workflow during PR checks.

### **How to Create a Quest**

1. Create a new repository by clicking on "Use this template" on the [quest template](https://github.com/trywilco/quest-template). This is a clone of the Funnel Drop quest and is fully playable as-is.
2. Update the quest files to support your new quest:
    1. Make sure to modify the `id` in `quest.yml` and specify a unique quest identifier.
    2. Use this documentation to modify the quest metadata and the logic of the steps.
3. Create a zip file from the quest files. You can use one of the following methods:
    1. Create a new release in your GitHub repository and download the zip asset generated for the release: [https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
    2. Manually zip the files located on your local machine.
    3. Auto-upload using Github Workflow :
        
        [Auto-Upload Quest Drafts](Quests%20Creation/Auto-Upload%20Quest%20Drafts.md)
        
        NOTE: Make sure you have Quests Editor permissions in Wilco.
        
4. Open the [my-quests](https://app.wilco.gg/my-quests) page and use the zip to upload a new quest. If you upload a new version for an existing quest, find the quest in the list and click the `Upload version` button.
5. Once the quest has finished uploading, click the `Test Quest in Snack` button and test the full quest flow.
6. When the quest is ready, click the `Submit for review` button.

### Quest Configuration Files

The uploaded zip must follow the following files structure:

```
quest.zip
├── quest.yml
│
├── assets
│   ├── cover.jpeg
│   └── logo.svg
├── steps
│   ├── <step_id_1>.yml
│   ├── <step_id_2>.yml
│   ├── ...
│   └── <step_id_n>.yml
└── tests
    ├── <test_file_name_1>
    ├── <test_file_name_2>
    ├── ...
    └── <test_file_name_n>
```

For full documentation on the quest files configuration files:

[Quest Configuration Files ](Quests%20Creation/Quest%20Configuration%20Files.md)

[Quest Resources](Quests%20Creation/Quest%20Resources.md)

### Triggers and Payload

Each trigger in the system generates a payload that is passed to actions and conditions blocks along with the global payload. When defining a call to action/condition block in the flow nodes, the developer specifies how to map a param from the payload to a param passed to the block.

For full specification:

[Triggers and Payload](Quests%20Creation/Triggers%20and%20Payload.md)

### Logic flow (FlowNode)

Each step consists of two logical parts

1. `startFlow`: logic to be performed when step starts. Usually includes sending instructions to the user from one of the bots. 
2. `trigger`: logic to be performed when the user performs a specific action. 

In both cases, the flow is defined using flow nodes. Each flow node consists of `do`, `if` and `switch` blocks. Each of them is built using actions and conditions.

For documentation on flow nodes:

[Flow Nodes](Quests%20Creation/Flow%20Nodes.md)

For documentation of all supported actions and conditions that can be used in the flows:

[Actions & Conditions APIs](Quests%20Creation/Actions%20&%20Conditions%20APIs.md)

### GitHub Actions

Each step that requires the user to open and merge a pull request (PR) can include the GitHub Actions configuration. These actions will run as part of a workflow triggered on every PR when the PR code changes. 

For full specification:

[GitHub Actions](Quests%20Creation/GitHub%20Actions.md)
