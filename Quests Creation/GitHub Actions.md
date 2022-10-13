# GitHub Actions

Each step that requires the user to open and merge a pull request (PR) can include the GitHub Actions configuration. These actions will run as part of a workflow triggered on every PR when the PR code changes. 

More on GitHub Workflows and GitHub Actions: [https://docs.github.com/en/actions/using-workflows](https://docs.github.com/en/actions/using-workflows).

Configuring GitHub Actions on a step is done by adding the `githubActions` key to the step YAML file. `githubActions` can include one or both of the keys, `backend` or `frontend`. Each allows configuring the actions for the specific part of the application.

```yaml
...

githubActions:
  backend:
    ...
  frontend:
    ...
```

**If either `backend` or `frontend` is missing from the configuration, no actions will be added for them.**

## Backend

If `backend` is specified in `githubActions`, a server will be loaded inside the Github Workflow environment. If a running server is required for `frontend` actions, but no additional configurations are required for the `backend`, an empty backend configuration must be added to the YAML.

The generated actions will install all required dependencies and run the server, both according to the current backend framework.

## Frontend

If `frontend` is specified in `githubActions` all frontend dependencies will be installed according to the current frontend framework.

## Configuration

Each part of the application can define the following configuration keys:

- `testFile`: A test file to be executed as part of the actions. This file must be placed in the `tests` folder of the quest file structure and is downloaded to the Github Workflow environment. The supported test file types are:
    - `js`: javascript file
    - `sql`: Structured Query Language files that contain code to work with relational databases
    
    Unless specified differently by the `capabilities` and/or `cmd` configuration, the test file will be executed using following default commands:
    
    - Backend: `node ${testFile}`
    - Frontend: `yarn test --ci --watchAll=false --silent ./${testFile}`
    
- `capabilities`: Capabilities are everything that is required to run the tests. The default behavior for `capabilities` is to install a library required by the test file. It means that the action generated will simply run the command `yarn add <capability>`.
    
    Some capabilities perform more complicated actions and are used to simplify the configuration of common behaviors:
    
    - `seeds`: Seeds the database with information for tests which require seeded data. This will generate an action according to the current backend database type.
    - `jest-puppeteer`: Frontend tests frequently require running [jest-puppeteer](https://jestjs.io/docs/puppeteer). If this capability is set, default `jest-puppeteer` configuration files will be downloaded to the workflow environment and the test command will be replaced with:
        
        `yarn run jest -c src/jest.config.js`
        
        The downloaded files are: 
        
        [https://engine.wilco.gg/quests/jest-puppeteer/jest-puppeteer.config.js](https://engine.wilco.gg/quests/jest-puppeteer/jest-puppeteer.config.js)
        
        [https://engine.wilco.gg/quests/jest-puppeteer/jest.config.js](https://engine.wilco.gg/quests/jest-puppeteer/jest.config.js)
        
- `cmd`: In most cases, using the default `capabilities` and test commands should be enough, but sometimes there is a need for custom commands. `cmd` can be either a single command or an array of commands. In any case, each command will add an action with the structure:
    
    ```json
    {
      "cmd": "<cmd>"
      "cwd": "backend | frontend",
    }
    ```
    

- `paramsFramework`: In some scenarios, tests should use different files or commands according to the used frameworks. `paramsFrameworks` is a map from framework type to `capabilities` and `cmd` keys.

## Examples

The following are a few examples of using GitHub Actions in steps YAML files:

---

```yaml
githubActions:
  backend:
    capabilities:
    - axios
    - dotenv
    testFile: "filter.js"
```

This will install `axios` and `dotenv` in the backend folder, download the test file `filter.js` and run the test using the default command `node filter.js`.

---

```yaml
githubActions:
  backend:
  frontend:
    capabilities:
    - jest-puppeteer
    - puppeteer
    testFile: "search-empty.test.js"
```

This will install `puppeteer` and `jest-puppeteer` in the frontend folder and, as `jest-puppeteer` capability is specified, will use `jest-puppeteer` to run the tests.

---

```yaml
githubActions:
  backend:
    capabilities:
    - autocannon
    - axios
    - seeds
    testFile: check_latency.js
```

This will install `autocannon` and `axios` and seed the database with information. Then the `check_latency.js` will be downloaded and test will run using the default command

 `node check_layency.js`

---

```yaml
githubActions:
  backend:
    capabilities:
    - seeds
    testFile: psql.sql
    cmd:
    - psql ${databaseUrl} -f ${testFile} -v ON_ERROR_STOP=1
    paramsFramework:     
      node:
        testFile: mongo.js
        cmd: 
          - mongo ${testFile}
```

In this example, we see the usage of both `paramsFramework` and `cmd` keys. The default test command does not work in this case, so `cmd` is used to specify a custom test command. Also, in case the backend framework is `node`, we use specific configurations for both the test file and the command.
