# Milestone 00: Running OpenEMR

## Learning Goals

By the end of this assignment, you will be able to:

- Explain what OpenEMR is and what problem it solves
- Set up a local development environment using Docker and Docker Compose
- Launch OpenEMR and log in to the web interface
- Navigate the basic structure of a large, real-world PHP application

## Background

OpenEMR is a widely used, open-source electronic health records (EHR) and
medical practice management system. It's a great codebase for learning how
large, real-world web applications are structured, deployed, and maintained.

In this assignment, you'll get OpenEMR running on your own machine using
Docker, so you have a working instance to explore in later assignments.

## Prerequisites

Before starting, make sure you have:

1. **Git** installed (`git --version` to check)
2. **Docker Desktop** installed and running
   - [Docker Desktop for Mac/Windows](https://www.docker.com/products/docker-desktop/)
   - On Linux, install Docker Engine + the Docker Compose plugin
3. At least **4 GB of free RAM** and **10 GB of free disk space** (OpenEMR's
   dev environment pulls several container images)
4. A terminal / command line you're comfortable using

Verify Docker is working:

```bash
docker --version
docker compose version
```

If either command fails, install/fix Docker before continuing — nothing
else in this assignment will work otherwise.

## Step 1: Clone the Repository

Clone **this** repository (not the original OpenEMR repo) — you'll be
working from the class fork/kit version:

```bash
git clone https://github.com/pfv610/OpenRE_Kit.git
cd <repo-folder-name>
```

## Step 2: Locate the Docker Setup

OpenEMR ships with a ready-made "easy" development Docker environment.
Navigate to it:

```bash
cd docker/development-easy
```

> **Note:** Open the `docker-compose.yml` file in this folder and skim it
> before continuing. Look for the `ports:` sections — these tell you which
> local ports the app, database admin tool, and mail catcher will be
> available on. Port numbers can vary between OpenEMR versions, so always
> check the file in your checked-out version rather than assuming.

## Step 3: Start the Containers

```bash
docker compose up -d
```

This will:
- Download several container images (OpenEMR, MariaDB/MySQL, phpMyAdmin, etc.)
- Start them all in the background (`-d` = detached mode)

**This can take several minutes the first time** — Docker needs to build
and initialize the database, install dependencies, and configure the app.
Grab a coffee.

Check that everything started correctly:

```bash
docker compose ps
```

You should see multiple services listed with a status of `Up` or `running`.

## Step 4: Log In to OpenEMR

Once the containers are up (give it 2–5 minutes after `docker compose up`
for first-time database initialization), open your browser to:

```
http://localhost:8300/
```

> If this port doesn't work, check the `docker-compose.yml` you reviewed in
> Step 2 for the actual host port mapped to the OpenEMR container's port 80/443.

Log in with the default development credentials:

- **Username:** `admin`
- **Password:** `pass`

If you see the OpenEMR dashboard, you're done! 🎉

## Step 5: Verify Your Setup

To confirm everything is working, do the following and take a screenshot:

1. Log in to OpenEMR as `admin`
2. Navigate to the **Patients** menu and add a new dummy patient
   (fake name, any DOB)
3. Save the patient and confirm it appears in the patient list

Submit a screenshot showing the patient you created in the list.

## Stopping the Environment

When you're done working, you can stop the containers without deleting
your data:

```bash
docker compose down
```

To start again later:

```bash
docker compose up -d
```

If you want to **completely reset** (delete all data and start fresh):

```bash
docker compose down -v
```

(The `-v` flag also removes the Docker volumes, which is where the
database lives.)

## Troubleshooting

| Problem | Likely Cause / Fix |
|---|---|
| `docker compose up` fails with a port conflict | Something else on your machine is using that port. Either stop that service, or edit the `ports:` section of `docker-compose.yml` to map to a different local port. |
| Page won't load / connection refused | The database may still be initializing. Wait a few more minutes and check `docker compose logs -f openemr` for progress. |
| Login fails with correct credentials | The database init may not have finished. Check `docker compose ps` — if a container keeps restarting, check its logs with `docker compose logs <service-name>`. |
| Docker Desktop won't start (Windows) | Ensure WSL2 is installed and enabled; Docker Desktop requires it. |
| Everything is very slow | Docker Desktop's default resource allocation may be too low — increase CPU/RAM limits in Docker Desktop settings. |

## Stretch Goal (Optional)

Once logged in, explore the codebase a bit:

- Find the folder where patient-related PHP code lives
- Find where the database schema/migrations are defined
- Look at `docker/development-easy/docker-compose.yml` again and identify
  what each service (container) is responsible for

No need to submit anything for this part — just get a feel for the codebase
before the next assignment.

## What to Submit

- Screenshot from Step 5 (dummy patient in the patient list)
- A short paragraph (3–5 sentences) describing any issues you ran into and
  how you resolved them (or if you had none, what you found confusing about
  the setup process)
