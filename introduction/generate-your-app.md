# Generate Your App

## Getting Started with UGF

For new users, please use [Yeoman ](https://yeoman.io/)tool to generate your first app:

Install Yeoman and clone UGF generator

```bash
#Install Yeoman
# Make sure both is installed globally
npm install -g yo
#Install UGF Generator
git clone https://github.com/a10networks/generator-ugf.git
cd generator-ugf
npm link
```

Generate your first project

```bash
# Create a new directory, and `cd` into it:
mkdir my-new-project && cd my-new-project

# Run the generator, and browser will open http://localhost:3000 automatically
yo ugf
```

Or you can use follow commands to boot up, build and test your project

```bash
# Start for development
npm start # or

# Just build the dist version and copy static files
npm run build

# Run unit tests
npm test
```

## Generate more

### Generate a container

```bash
# cd my-new-project
yo ugf:container my/namespaced/container
```

### Generate a component

```text
# cd my-new-project
yo ugf:component my/namespaced/container
```

### Generate an feature

```bash
# TO DO: generate a dashboard or a wizard or other apps
# yo ugf:dashboard my/namespaced/dashboard
```

## To generate more?

To use the generator generate more , please read generator-ugf [Readme.md ](https://github.com/a10networks/generator-ugf)



