# heroku_frontend

Description: Heroku app hosting the frontend

When specified as a resources, a fully functional Heroku app will be created for the frontend and configured for the user. 

Supported properties:

- **clear:** allows clearing specific configurations from an already-existing Heroku app.
    - config_vars: list of config vars to be removed.
    - buildpacks: list of buildpacks to be removed.

```yaml
resources:
- name: heroku_frontend
  clear:
    config_vars:
    - REACT_APP_BACKEND_URL
    - PROJECT_PATH
    buildpacks:
    - https://github.com/timanovsky/subdir-heroku-buildpack
    - https://buildpack-registry.s3.amazonaws.com/buildpacks/mars/create-react-app.tgz
    - https://github.com/mars/create-react-app-buildpack
```

In this example, a Heroku app will be prepared and configured to work with the user’s app frontend. If such an app exists, the keys `REACT_APP_BACKEND_URL` and `PROJECT_PATH` will be removed along with the specified buildpacks.
