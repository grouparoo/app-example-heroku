# app-example-heroku

Example Grouparoo project for deploying Grouparoo on Heroku.

Goal: To create a scalable and flexible Grouparoo deployment that:

- Has no servers to directly manage
- Can be auto-scaled as needed
- Will be automatically deployed when the code changes
- Is a [12-factor app](https://12factor.net/) with all configuration stored in the Environment

## Repository Configuration

1. Create a new Grouparoo project. Learn more @ https://www.grouparoo.com/docs/installation.

```
npm install -g grouparoo
grouparoo init .
```

2. Install the Grouparoo plugins you want, e.g.: `grouparoo install @grouparoo/postgres`. Learn more @ https://www.grouparoo.com/docs/installation/plugins

3. Create the `Procfile` to enable both `web` and `worker` dynos.

```
web:    cd node_modules/@grouparoo/core && WEB_SERVER=true  WORKERS=0  ./bin/start
worker: cd node_modules/@grouparoo/core && WEB_SERVER=false WORKERS=10 ./bin/start
```

## Deployment Steps

1. Create a new Heroku app with `Heroku Postgres` and `Heroku Redis`. Heroku will automatically configure the environment variables `DATABASE_URL` and `REDIS_URL` for you.
2. Configure Heroku to automatically deploy the `main` branch of your repository.

## Alternative Deployment

Click this button to deploy a copy of this repository!

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/grouparoo/app-example-heroku)

## Notes

- Heroku uses a `Procfile` to define the `web` and `worker` dynos.
- This repo also powers the `Deploy with Heroku` button, so there's an `app.json` file to configure that deployment. You won't need that in your project.
