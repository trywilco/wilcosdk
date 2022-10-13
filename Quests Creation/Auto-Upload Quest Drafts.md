# Auto-Upload Quest Drafts

To simplify the process of uploading draft versions, quest developers can configure their repo to upload an updated version after pushing new code to the `main` branch.

1. First, you will need to generate a Quest Developer token. Open the [my-quests](https://app.wilco.gg/my-quests) page and find the `More Options` button (three vertical dots). Select the `Generate New Token` option and follow the instructions to create a new token.
2. Add the token to the quest repo secrets:
    1. Open quest repo settings.
    2. Tap `Secrets` on the left panel and select `Actions` in the drop-down.
    3. Tap the `New Repository Secret` button.
    4. Name the new secret `QUESTS_EDITOR_TOKEN` and copy the token to the `secret` text box. 
3. Add a new workflow file to the GitHub repo:
    1. If you used the quest template, the file is already a part of the repo and needs to be configured. The file is located in `.github/workflows/upload-draft.yml`. Open the file and modify the value of the key `quest-editor-user-email` to be your Wilco login email address.
    2. If the file is not part of your repo, you can generate it by tapping the `More Options` button on the my-quests page and selecting `Download Github Workflow`. Copy the generated file to your repo inside the folder `.github/workflows/`. No additional modifications to the file are required.