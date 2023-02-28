## Dockerizing a React App

## Step 1 - Create React App

Create simple create app by using this command `npx create-react-app project_name`

## Step 2 - Add a .dockerignore File

Just like .gitignore file, use .dockerignore for ignoring files while building process.
As a simple example `node_modules` is the folder which is usually excluded.

## Step 3 - Add a Dockerfile

To give instructions, it's needed to create a docker file
Example `Dockerfile` without extension, but also with a capital `D`

## Step 4 - Add instructions

Since react is not a node application, first of all it's neeeded to import node
Example `FROM node:19-alpine`. After `:` you specify the version of node.
Note: Using `alpine` flavour of an image (e.g. `node:16-alpine` instead of `node:16`) will give you a smaller image size

Then you should define a working directory
Example `WORKDIR /app`

After that, package.json and .lock file should be copied. Otherwise, we won’t be able to use npm commands in the next layer. These files should be copied to the working directory which we defined above. For that, we add a `.` after the copy command. But copying the .lock file is not required. You can exclude
Example `COPY package.json .`

In the next step, we have to install all the dependencies which we used in the project.
Example `RUN npm install`

Then we need to copy the rest of the content to the working directory
Example `COPY . .`

Finally starting an application
Example `CMD ["npm", "start"]`

## Step 5 - Create a docker image

To create a docker image, copy this command into your terminal
Example `docker build . -t <image_name>`

## Viewing the image

To view the image you can use `docker images` or `docker image ls` in your terminal.
Also you can use Docker GUI to view the created image

## Running the image

If you want to run the image, use `docker run <image_name>`
Then you can open new window in terminal and see the list of images by using this command `docker ps`

## Execute the container

To execute it, use `docker exec -it <image_id> sh`
Now you are able to use `npm start` inside.
