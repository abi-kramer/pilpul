# Running Pilpul Locally

This guide will describe the pre-requisites, setup, and startup instructions that are involved with deploying a local Pilpul instance.

## Pre-Requisites

Running this project locally assumes that [Docker Desktop](#docker-desktop), [Supabase](#supabase), and [Node.js](#nodejs) have been installed.

### Docker Desktop

Docker Desktop is the most popular option, but any Docker API container manager is acceptable (e.g. Docker Desktop, Rancher Desktop, Podman, etc.) Follow the installation instructions for the container manager of choice, and ensure it is running in the background by running `docker ps`.

### Supabase

Follow the OS-specific installation instructions for local development available [here](https://supabase.com/docs/guides/local-development/cli/getting-started)

### Node.js

Follow the OS-specific installation instructions for installing Node.js and npm available [here](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm?library=true)


## Environment Variables

A `.env` file must be present in the main project directory in order for the project to be started. The table below outlines the possible environment variables that can be defined. At minimum the two required variables must be populated.

| Variable                     | Description                                                                                  | Required |
|------------------------------|----------------------------------------------------------------------------------------------|----------|
| SUPABASE_URL                 | The Project URL of the running Supabase instance                                             | yes      |
| SUPABASE_SERVICE_ROLE_KEY    | The service role (Secret) key from the instantiated Supabase instance                        | yes      |
| SUPABASE_ANON_KEY            | The anon role (Publishable) key from the instantiated Supabase instance                      | no       |
| MAINTAINER_EMAILS            | The email to be associated as a maintainer for the running application                       | no       |
| RESEND_API_KEY               | If running Resend, the generated API key for request authentication                          | no       |
| RESEND_FROM_EMAIL            | If running Resend, the email that will send email authentication links                       | no       |
| APP_ORIGIN                   | The base URL of the running application, necessary when using email authentication links     | no       |
| ALLOW_DEV_MAGIC_LINKS        | true or false, whether or not to allow magic links (via Resend), when running a dev instance | no       |
| ALLOW_UNVERIFIED_EMAIL_CLAIM | true or false, whether or not to allow unverified email claims                               | no       | 


## Project Startup

### Starting Supabase

Before starting Pilpul, a local instance of Supabase must be started for backend support. In the main project directory, a Supabase project has been initialized (see `./supabase/config.toml`). Run the command `npx supabase start` (if installed with npm) or `supabase start` (if installed with brew) to start this initialized instance. 

Running this command will provide output in the terminal that can be referenced for development use. The Supabase Project URL will by configuration be `http://127.0.0.1:54321`. This will be the `SUPABASE_URL` environment variable value in the created `.env` file. The other two values that can be filled in at this point are `SUPABASE_SERVICE_ROLE_KEY` (this will start with "sb_publishable") and `SUPABASE_ANON_KEY` (this will start with "sb_secret"). 

These values are also retrievable by navigating to the Supabase Studio (`http://127.0.0.1:54323`), or by running `supabase status`.

## Starting Pilpul

To start the Pilpul instance, run the following:

1. `npm install`
2. `npm run dev`

This will start Pilpul on `http://localhost:5000`.

### Logging in Locally

From the home page at `http://localhost:5000`, enter any email (doesn't have to be a real one, it just has to follow the name@domain.com convention). With it being local development, a local sign-in link will appear to click on to 'log in' to Pilpul.

### Creating a Room

Once logged in, you can select to create a room. From here you can title the text, upload a PDF, and select the pace, commitment level, and language. After selecting to create an invite link, the link can be opened.

### Creating a Fake User

<!-- TODO: clarify steps upon login - appears that /api/demo/seed-partner is called upon instantiation? -->

Once logged in, you can select to find another partner, fill in the required fields, then select to enter the queue.

To experience the session room solo, create a request from `/find`, land on `/queue`, then call:

```bash
POST /api/demo/seed-partner
```

```bash
curl -X POST http://localhost:5000/api/demo/seed-partner
```

## Using Resend

<!-- TODO: document how to link resend into local devlopment -->

