# Setup

```bash
docker-compose up
```
then 

open 

http://localhost:10880

in your browser

# Initial setup screen (Browser)

- Database type: SQLite3
- Application URL: http://localhost:10880/
- Enable console mode

In terminal 

Open a shell into the gogs container

```bash
docker run -it <containerid> /bin/bash
```

Then in the bash session in the container run the following to create 3 new users

```bash
su git
./gogs admin create-user --name <username> --password <password> --email <emailaddress>
./gogs admin create-user --name <username2> --password <password2> --email <emailaddress2>
./gogs admin create-user --name admin1 --password password --email admin1@example.com --admin
```

Then in your browser go to

http://localhost:10880/user/login

And log in with the credentials you just created

# Create 1st repository

Log into gogs as admin 1
Create repository in gui called hello-world
Choose the Nodejs gitignore template
Choose to create initial files

# Pull from 1st repository

```bash
mkdir development
cd development
git clone http://localhost:10880/admin1/hello-world.git ./machine1
git clone http://localhost:10880/admin1/hello-world.git ./machine2
cd machine1
git config credential.helper 'store --file ~/.hello-world_credentials'
cd ..
cd machine2
git config credential.helper 'store --file ~/.hello-world_credentials'
```

In the local working copy in machine1 run

```bash
npm init -y
```

Enable ES Modules in the package.json

Then run

```bash
npm i express
npm i --save-dev jest nodemon
touch index.js
node_modules/jest/bin/jest.js --init
mkdir __tests__
```

## Jest init answers

```bash
✔ Would you like to use Jest when running "test" script in "package.json"? … yes
✔ Would you like to use Typescript for the configuration file? … no
✔ Choose the test environment that will be used for testing › node
✔ Do you want Jest to add coverage reports? … no
✔ Which provider should be used to instrument code for coverage? › v8
✔ Automatically clear mock calls, instances, contexts and results before every test? … yes
```

## Add Repository Collaborators

In your browser go to 

http://localhost:10880/admin1/hello-world/settings/collaboration

And add the users

- charlie
- chris

## Charlie to push changes from machine1

```bash
git add .
git commit -m "Initial commit"
git push
```

Supply user name and password when prompted

## Chris to pull change from repo to machine2

```bash
cd ../machine2
git pull
npm i
npm start
```