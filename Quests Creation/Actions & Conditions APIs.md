# Actions & Conditions APIs

This page explains how actions and conditions work and documents all actions and conditions supported. This document assumes the reader is familiar with how [Triggers and Payload](Triggers%20and%20Payload.md) works

## Actions - General

Actions are part of `do` statements and are used to change the state of the user in the game or to give the user information or guidance. Some actions also add information to the payload `outputs` to be used by other conditions or actions. A common example for this is setting `success` and `error` in case of a failure. 

In case `name` is set for the action, `outputs.<action_name>.success` will always be set and will default to `true` unless the action changed it.

Actions support the following params:

| Name | Type | Mandatory | Default | Description |
| --- | --- | --- | --- | --- |
| actionId | String | YES | - | String representing the actions. See section below for supported actions ids. |
| name | String | NO | null | Name is mandatory in order to use action outputs. If name is specified and action enriches payload outputs, it can be accessed using:
${outputs.<action_name>.<param_name>}. |
| params | Map | NO | null | Each action specifies which params it requires. Some params are passed transparently from the trigger payload and some must be configured. |
| paramsFramework | Map | NO | null | Used in cases framework selected by the user affects the params passed to the action. It is a map from framework name to params.|

Example:

```yaml
do:
- actionId: bot_message
  params:
    person: devops
    messages:
    - text: "Great! Next, it might be a good idea to go ahead and **clone that repository**, before doing any other tasks. *Clone it*, don't fork it!"
      delay: 3000
    - text: "\"It might be\" as in - you should definitely do it **before doing any of your next tasks**."
      delay: 2000
    - text: "When you're done, *talk to ${bots['head-of-rd'].displayName}*, she’ll take it from here."
      delay: 2500
- actionId: finish_step
```

In this simple example two actions are performed. The first sends messages from a bot the user and the second progressed the user to the next step.

Another example:

```yaml
- actionId: newrelic_configure_with_key
  name: newrelic_configure_with_key
  params:
    newRelicKey: "${userMessageText}" #userMessageText is text sent to a bot by the user 
```

In this example, the action `newrelic_configure_with_key` might fail with several error types. A name is set in order to fetch the error type:

```yaml
switch:key: "${outputs.newrelic_configure_with_key.error}"
  cases:
    invalid_key_format:
      do:
      ...
    invalid_key:
      do:
      ...
```

## Conditions - General

Condition and part of `if` statements are used to check user’s state in order to decide how to progress. Some conditions also add information to the payload `outputs` to be used by other conditions or actions. In case `name` is set for condition, `outputs.<conditions_name>.success` will always be set.

Conditions support the following params:

| Name | Type | Mandatory | Default | Description                                                                                                                                                                           |
| --- | --- | --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| conditionid | String | YES | - | String representing the condition. See section below for supported condition ids.                                                                                                     |
| equals | Object | NO | true | condition is successful if its return value equals to equals. Common usage is to evaluate the negation of the condition by setting equals: false.                                     |
| name | String | NO | null | Name is mandatory in order to use condition outputs. If name is specified and condition enriches payload outputs, it can be accessed using: ${outputs.<condition_name>.<param_name>}. |
| params | Map | NO | null | Each condition specifies which params it requires. Some params are passed transparently from the trigger payload and some must be configured.                                         |
| paramsFramework | Map | NO | null | Used in cases framework selected by the user affects the params passed to the condition. It is a map from framework name to params.                                                   |
| onFalseParams | Map | NO | null | Params to set on the global payload in case condition is unsuccessful. Common usage is list of conditions, each having its error message to be sent by the bot in case of a failure.  |

Example:

```yaml
if:
  conditions:
  - conditionId: github_is_file_modified
    params:
      defaultResult: true
    paramsFramework:
      node:
        fileName: backend/app.js
    onFalseParams:
      pr_reject_message: "Did you make sure you added the `require` statement to the main app file?"
      pr_reject_message_name: "missing_require"

  - conditionId: github_is_file_modified
    params:
      defaultResult: true
    paramsFramework:
      python:
        fileName: backend/Procfile
    onFalseParams:
      pr_reject_message: "Looks like you did not update the `Procfile`. Remember you need to add the New Relic admin script command in front of your usual startup command options."
      pr_reject_message_name: "procfile_not_updated"

  - conditionId: github_is_file_modified
    params:
      defaultResult: true
    paramsFramework:
      node:
        fileName: backend/package.json
      rails:
        fileName: backend/Gemfile
      python:
        fileName: backend/requirements.txt
    onFalseParams:
      pr_reject_message: "Did you add the New Relic package to the dependency list? Make sure to add it to the **backend** project."
      pr_reject_message_name: "missing_dependency"

  - conditionId: github_is_file_added
    params:
      defaultResult: true
    paramsFramework:
      node:
        fileName: backend/newrelic.js
      rails:
        fileName: backend/config/newrelic.yml
      python:
        fileName: backend/newrelic.ini
    onFalseParams:
      pr_reject_message: "I don’t see a New Relic config file. Won’t work without it."
      pr_reject_message_name: "missing_config"

  - conditionId: github_is_file_contains
    equals: false
    params:
      regex: license_key
      defaultResult: false
    paramsFramework:
      node:
        fileName: backend/newrelic.js
      rails:
        fileName: backend/config/newrelic.yml
      python:
        fileName: backend/newrelic.ini
    onFalseParams:
      pr_reject_message: "I see you've committed a license key to Git. Shouldn't do that, security-wise. Please remove the entire property from the config file, we'll add it as an environment variable."
      pr_reject_message_name: "committed_license_key"

  - conditionId: github_is_file_added
    equals: false
    params:
      defaultResult: false
    paramsFramework:
      node:
        fileName: backend/package-lock.json
    onFalseParams:
      pr_reject_message: "I see you have both `package-lock.json` and `yarn.lock`. This can cause issues in the build. Let’s stick with just yarn for now, and remove the `package-lock.json`."
      pr_reject_message_name: "npm_lock_added"

  then:
    do:
    - actionId: bot_message
      params:
        person: devops
        messages:
        - text: "Looking good! You can merge the PR now."
          delay: 1000
    - actionId: github_pr_approve
      params:
        person: devops
        message: "Looking good! You can merge the PR now."

  else:
    do:
    - actionId: bot_message
      params:
        person: devops
        messages:
        - text: "${pr_reject_message}"
          delay: 1000
    - actionId: github_pr_reject
      params:
        person: devops
        message: "${pr_reject_message}"
        messageName: "${pr_reject_message_name}"
```

In this example, we see an `if` statement with several conditions. If all conditions are successful, a message is sent by the bot and PR is approved. If a condition fails, PR is rejected with a rejection message. The message text is set by each condition using `onFalseParams`.

Note the use of `equals: false` and the use of `paramsFramework` in this example.

## Supported Actions and Conditions


| Name                                                                                                               | Category | Type      | Description | More Info |
|--------------------------------------------------------------------------------------------------------------------|----------|-----------| --- | --- |
| [text_contains_strings](Actions%20&%20Conditions%20APIs/text_contains_strings.md)                                  | String   | Condition | Check if text contains subset of strings |
| [text_match_regex](Actions%20&%20Conditions%20APIs/text_match_regex.md)                                            | String   | Condition | Check if text matches regex |
| [is_user_message_text_ready_to_continue](Actions%20&%20Conditions%20APIs/is_user_message_text_ready_to_continue.md) | Chat     | Condition | Check if user answered both with message that means they are ready to continue |
| [bot_message](Actions%20&%20Conditions%20APIs/bot_message.md)                                                      | Chat     | Action    | Send message from user to a bot |
| [user_check_authentication_exists](Actions%20&%20Conditions%20APIs/user_check_authentication_exists.md)            | General  | Condition |  |
| [github_is_user_valid](Actions%20&%20Conditions%20APIs/github_is_user_valid.md)                                    | Github   | Condition | Check if username exists in Github |
| [github_is_file_modified](Actions%20&%20Conditions%20APIs/github_is_file_modified.md)                              | String   | Condition | Check if specified file was modified as part of PR changes |
| [github_is_one_of_files_modified](Actions%20&%20Conditions%20APIs/github_is_one_of_files_modified.md)              | Github   | Condition | Check if one of specified files was modified as part of PR changes |
| [github_is_file_add](Actions%20&%20Conditions%20APIs/github_is_file_add.md)                                        | Github   | Condition | Check if specified files was added as part of PR changes. |
| [github_is_file_contains](Actions%20&%20Conditions%20APIs/github_is_file_contains.md)                              | Github   | Condition | Check if file added in PR contains text that matches a regex |
| [github_is_repo_collaborator](Actions%20&%20Conditions%20APIs/github_is_repo_collaborator.md)                      | Github   | Condition | "Check if user accepted the invitation for his repo. " |
| [github_is_file_added_in_push](Actions%20&%20Conditions%20APIs/github_is_file_added_in_push.md)                    | Github   | Condition | Check if a file was added in the head commit of a git push (not specific to a PR) |
| [github_create_repo](Actions%20&%20Conditions%20APIs/github_create_repo.md)                                        | Github   | Action    | Create new repo for the user. |
| [github_invite_user](Actions%20&%20Conditions%20APIs/github_invite_user.md)                                        | Github   | Action    | Invite user to collaborate on Github repo. |
| [github_pr_comment](Actions%20&%20Conditions%20APIs/github_pr_comment.md)                                          | Github   | Action    | Add comment on a PR on behalf of one the bots. |
| [github_pr_approve](Actions%20&%20Conditions%20APIs/github_pr_approve.md)                                          | Github   | Action    | Approve the PR and add comment on behalf of a bot. |
| [github_pr_reject](Actions%20&%20Conditions%20APIs/github_pr_reject.md)                                            | Github   | Action    | Reject the PR and add comment on behalf of a bot. |
| [github_open_issue](Actions%20&%20Conditions%20APIs/github_open_issue.md)                                          | Github   | Action    | Opens an issue in the user’s Github repository |
| [heroku_check_backend_config_var](Actions%20&%20Conditions%20APIs/heroku_check_backend_config_var.md)              | Heroku   | Condition | Check if config variable is set (exists) for the backend Heroku app. |
| [heroku_check_frontend_config_var](Actions%20&%20Conditions%20APIs/heroku_check_frontend_config_var.md)            | Heroku   | Condition | Check if config variable is set (exists) for the frontend Heroku app. |
| [newrelic_license_key_valid](Actions%20&%20Conditions%20APIs/newrelic_license_key_valid.md)                        | NewRelic | Condition | Check if given key is a valid new relic license key. |
| [newrelic_configure_with_key](Actions%20&%20Conditions%20APIs/newrelic_configure_with_key.md)                      | NewRelic | Action    | Configure user New Relic properties using given license key |
| [action_success](Actions%20&%20Conditions%20APIs/action_success.md)                                                | General  | Condition | Check if the previously executed action block finished with success |
| [network_http_request](Actions%20&%20Conditions%20APIs/network_http_request.md)                                    | Network  | Action    | Perform http request |
| [is_truthy](Actions%20&%20Conditions%20APIs/is_truthy.md)                                                          | General  | Condition | Test if expression is truthy |
| [is_falsy](Actions%20&%20Conditions%20APIs/is_falsy.md)                                                            | General  | Condition | Test if expression is falsy |
| [database_check_connection_url](Actions%20&%20Conditions%20APIs/database_check_connection_url.md)                  | Database | Condition | Verify if database connection url is valid |
| [array_find](Actions%20&%20Conditions%20APIs/array_find.md)                                                        | Array    | Condition | Find an element in the array that matches specified conditions |
| [array_every](Actions%20&%20Conditions%20APIs/array_every.md)                                                      | Array    | Condition | Tests whether all elements in an array pass specified conditions |
| [finish_step](Actions%20&%20Conditions%20APIs/finish_step.md)                                                      | Quest    | Action    | Advance user to next step or finish quest in case this is the last step |


[Text Formatting](Actions%20&%20Conditions%20APIs/Text%20Formatting.md)
