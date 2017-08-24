# Docker image for deploying create-react-app Apps easily

A Docker image that builds a create-react-app app from source and deploys it to an NGinx server

## Building your Image

- Create a *Dockerfile* with the follwing line under the `src` folder, in the same level as the *package.json*.:
```
FROM tiagostutz/create-react-app-ngnix
```
- Build your image running the command `docker build -t [your_image_name] .` in the folder that the *Dockerfile* and *package.json* are placed.
- Startup your app: `docker run -d -p 8000:80 [your_image_name]`
- Try in your browser at `localhost:8000`

----

Folder structure:

```
| |____Dockerfile
| |____package.json
| |____public
| | |____favicon.ico
| | |____index.html
| | |____manifest.json
| |____README.md
| |____src
| | |____App.css
| | |____App.js
| | |____App.test.js
| | |____index.css
| | |____index.js
| | |____logo.svg
| | |____registerServiceWorker.js
```
