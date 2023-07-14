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