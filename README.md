# React app
1. Install node.js
2. Node -v 
3. npm install -g create -react-app  // using this tool to generate an react-app
4. npm run start -> to start a development server for dev only
5. npm run test -> runs tests associated with the project
6. npm run build -> builds a production version of the application 
7. Dev build : Dockerfile.dev 
    docker build -f dockerfile.dev .
8. docker run -p 3000:3000 bf9ba1744048  <-- the image id it build from the above command
9. docker run -p 3000:3000 -v /app/node_modules -v  $(pwd):/app  <image_id>

10. Or instead using the long docker command each time, 
use the docker-compose.yml + following commands, note - the docker-compose.yml file, with the local file linked to the container and changes are hot deploy to the container. 

docker-compose up
docker-compose down


 11. Running tests
    - docker run -it 673467c9eb4b npm run test

    or 
    1st cmd 
    - docker-compose up
    2nd cmd
    - docker ps to find out the conatainer id
    - docker exec -it <container_id> npm run test

    you can see the test run in the container. then you can add or remove tests on locel App.test.js, then re-run the test without exiting the container to observe how the the test are live update

    OR using docker compose to run the test, but losig the ability for special commands , P, W , Q, S
    Look at the second services in the docker compose file. 

12. Production Version of the app using ngix
    Dockerfile 
    Use node:alpine -> copy the package.json file > install dependencies (? deps only needed to execute 'npm run build') > Run 'npm run build' > start nginx (? where's nginx comning from??)

    Docker file prod
    Build phase: use node: alpine > copy the package.json file > install dependencies > run 'npm run build'

    Run Phase: use nginx > copy over the result of 'npm run build' > start nginx

    a. add the Dockerfile
    b. docker build .
    c. docker run -p 8080:80 <image_id>    


______________________________________________________________________
Feb 28

0. to check out the project git clone https://github.com/lotary/docker-react.git

1. Setting up the CI-CD

git init git add . git commit -m "initial commit" git remote add origin "https://github.com/lotary/docker/edit/master/prod/frontend"

integrate the github repo with Travis CI 1. create account in Travic , 2. allow Travis CI to integrate with the repo, 3. create the .travis.yml file to instruct travis CI for automate build

