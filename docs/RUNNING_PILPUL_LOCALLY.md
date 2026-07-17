# Running Pilpul Locally


## Pre-Requisites

Running this project locally assumes that [Docker Desktop](#docker-desktop), [Supabase](#supabase), and [Node.js](#nodejs) have been installed.

### Docker Desktop

Docker Desktop is the most popular option, but any Docker API container manager is acceptable (e.g. Docker Desktop, Rancher Desktop, Podman, etc.) Follow the installation instructions for the container manager of choice, and ensure it is running in the background by running `docker ps`.

### Supabase

Follow the OS-specific installation instructions for local development available [here](https://supabase.com/docs/guides/local-development/cli/getting-started)

### Node.js

Follow the OS-specific installation instructions for installing Node.js and npm available [here](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm?library=true)



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


