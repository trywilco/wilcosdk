# Quest Configuration Files

Every uploaded quest must include a file called `quest.yml` that configures the metadata of the quest, an `assets` folder with cover and logo images, and a `steps` folder with a yaml file for each step. In addition, a `tests` folder can be added with test files to be used by the steps.

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

## quest.yml

This is a mandatory file that must be placed at the root of the zip archive's structure. This file defines the metadata of the quest:

```yaml
id: a unique quest identifier. Should not change. 3-50 characters, must begin with a letter. Accepted characters are A-Z, a-z, 0-9, and "_" | mandatory
title: Quest title. 2-80 characters. All characters are accepted. "Funnel Drop" in the sample below | mandatory
description: Quest description. All characters are accepted. "What's worse.." in the sample below | mandatory
slogan: Quest slogan. 2-1000 characters. "It's time for.." in the sample below | mandatory
level: Quest level. beginner/intermediate/advance | mandatory
duration: Estimated number of hours required to finish the quest | mandatory
resources: A list of resources that should be avaiable to the user when quest begins | optional 
- resource_1
- resource_2
- ...
- resource_n
steps: List of all quest step ids | mandatory
- step_id_1
- step_id_2
- ...
- step_id_n
skills: List of skills the user will work on when playing the quest | mandatory
- skill_1
- skill_2
- ...
- skill_n
questDependency: Quest that must be complete before playing this quest | optional
```

[Supported Skills](Quest%20Configuration%20Files/Supported%20Skills.md)

[Quest Resources](Quest%20Resources.md)

![Screen Shot 2022-09-06 at 22.37.35.png](Quest%20Configuration%20Files/Screen_Shot_2022-09-06_at_22.37.35.png)

## Steps

This is a mandatory folder containing a file for each step defined in `quest.yml` file. There are no rules regarding the file names.

```yaml
id: Step id as specified in quest.yml file | mandatory
learningObjectives: Bulletpoints stating what users will learn to do in the quest | mandatory
- learning_objective_1
- learning_objective_2
- ...
hints: List of hints to give the user when they are stuck | optional
- hint_1
- hint_2
- ...
- hint_n
startFlow: Flow node logic to execute when the step begins | optional
	...
trigger: Trigger type and flow node logic. Each step has one trigger | mandatory
  type: Type of trigger (user action) the step waits for
  flowNode: Flow node logic to execute when user perform the action | mandatory
    ...
githubAction: Github Actions configuration to run in opened PRs | optional
```

[Triggers and Payload](Triggers%20and%20Payload.md)

[Flow Nodes](Flow%20Nodes.md)

[Actions & Conditions APIs](Actions%20&%20Conditions%20APIs.md)

## Assets

The assets folder contains images that are required to present the quest in the catalog or in the list of users’ quests. The folder and the files are mandatory. 

Supported image extensions:

- png
- jpg / jpeg
- gif
- svg

The following files must be placed in the assets folder:

- **cover:**  The main cover image of the quest, shown in the catalog. The name of this file must be `cover`.
    
    ![Screen Shot 2022-09-06 at 23.53.34.png](Quest%20Configuration%20Files/Screen_Shot_2022-09-06_at_23.53.34.png)
    
- **logo**: The logo image presented when selecting a quest from the catalog. The name of this file must be `logo`.
    
    ![Screen Shot 2022-09-06 at 23.53.48.png](Quest%20Configuration%20Files/Screen_Shot_2022-09-06_at_23.53.48.png)
    

### tests

The tests folder is optional and contains test files to be accessed by GitHub Actions.

For information on supported file types and usage:

[GitHub Actions](GitHub%20Actions.md)
