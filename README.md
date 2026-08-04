# Getting started with Docker

This repository is a sample application for users following the getting started guide at https://docs.docker.com/get-started/.


## Start the app

1. Open a terminal in the project folder:
   ```bash
   cd /home/gus/Docker/getting-started-app
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the application:
   ```bash
   npm run dev
   ```

4. Open the app in your browser:
   ```text
   http://127.0.0.1:3000/
   ```

## Run with Docker

If you prefer to run the app in a container, use:

```bash
docker build -t getting-started-app .
docker run -p 3000:3000 gustavdhub/getting-started
```
## Create volume
```bash
docker volume create todo-db
```
##  Mount volume
```bash
docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos gustavdhub/getting-started
```


---

## Submodule: awesome-compose

This repository includes a git submodule at `awesome-compose` that points to the upstream Docker "awesome-compose" examples repository. The submodule is declared in `.gitmodules`:

```gitconfig
[submodule "awesome-compose"]
	path = awesome-compose
	url = https://github.com/docker/awesome-compose.git
```

Why it is a submodule
- The `awesome-compose` examples are maintained in a separate repository and are tracked here as a submodule to keep their history and updates separate from this repo.

How to clone and initialize the submodule
- Clone and initialize the submodule in one step:

```bash
git clone --recurse-submodules https://github.com/gus-hub-tech/docker.git
```

- Or clone first, then initialize and fetch submodules:

```bash
git clone https://github.com/gus-hub-tech/docker.git
cd docker
git submodule update --init --recursive
```

Working with the submodule
- To update the submodule to the commit recorded in this repository:

```bash
git submodule update --init --recursive
```

- To pull the latest changes from the submodule's upstream repository (note: this will advance the submodule commit locally but you must commit the change in the superproject to persist it):

```bash
cd awesome-compose
git pull origin main
cd ..
# then in the superproject
git add awesome-compose
git commit -m "Update awesome-compose submodule"
```

CI / automation
- If you use GitHub Actions or other CI, ensure submodules are fetched. Example `actions/checkout` configuration:

```yaml
- uses: actions/checkout@v3
  with:
    submodules: true
    fetch-depth: 0
```

Removing or vendoring the submodule
- If you prefer the `awesome-compose` files to live directly in this repo instead of as a submodule, you can either remove the submodule and copy in the files, or use `git subtree` to import the repository history. Ask me if you want a step-by-step PR to vendor the examples instead.

If you'd like, I can open a PR that adds this README section instead of committing directly. I added this note to the README so contributors and CI users know how to clone and work with the submodule.