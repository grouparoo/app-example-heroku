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

3. Create the `Procfile` to enable both `web` and `worker` dynos.  We are running the same code, but using in-line environment varaibles to configure if the instance should boot as a web server or worker.

```
web:    cd node_modules/@grouparoo/core && WEB_SERVER=true  WORKERS=0  ./bin/start
worker: cd node_modules/@grouparoo/core && WEB_SERVER=false WORKERS=10 ./bin/start
```

## Deployment Steps

1. Create a new Heroku app with `Heroku Postgres` and `Heroku Redis`. Heroku will automatically configure the environment variables `DATABASE_URL` and `REDIS_URL` for you. We recommend:
   - at least `standard` Dynos
   - at least `standard2` for the Postgres Database
   - at least `premium0` for the Redis Database
2. Configure Heroku to automatically deploy the `main` branch of your repository.
3. Configure the following environment variables:
   - `DATABASE_SSL_SELF_SIGNED=true` - The lower tier of Heroku databases use self-signed SSL certificates
   - `GROUPAROO_LOGS_STDOUT_DISABLE_TIMESTAMP=true`- Heroku adds timestamps to all log messages
   - `GROUPAROO_LOGS_STDOUT_DISABLE_COLOR=true`- Heroku will not render log messages in color

## Alternative Deployment

Click this button to deploy a copy of this repository!

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/grouparoo/app-example-heroku)

## Notes

- Heroku uses a `Procfile` to define the `web` and `worker` dynos.
- This repo also powers the `Deploy with Heroku` button, so there's an `app.json` file to configure that deployment. You won't need that in your project.

---

Vist https://github.com/grouparoo/app-examples to see other Grouparoo Example Projects.
