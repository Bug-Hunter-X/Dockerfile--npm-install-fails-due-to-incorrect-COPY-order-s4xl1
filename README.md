# Dockerfile Bug: npm install Failure

This repository demonstrates a common error in Dockerfiles where the `npm install` command fails due to an incorrect order of the COPY instruction.

## Bug Description
The original `Dockerfile` has the `COPY package*.json ./` instruction before the  `COPY . .` instruction. This causes the `npm install` command to fail because it can not find the `package*.json` file. 

## Solution
The solution involves moving the `COPY . .` command before the `RUN npm install` to ensure that all the files are present when the installation begins. 

## How to reproduce the bug
1. Clone this repo.
2. Build the image with the original `Dockerfile`:
   ```bash
   docker build -t buggy-app .
   ```
3. You'll see that the build fails.

## How to fix the bug
1. Use the `DockerfileSolution.txt` file to build the image.
2. Build the image with the solution `Dockerfile`:
   ```bash
   docker build -t fixed-app -f DockerfileSolution.txt .
   ```
3. This time it should build successfully.
