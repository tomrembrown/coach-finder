# Coach Finder

This is a website built to find coaches and send them messages. It is built based on the Vue - The Complete Guide - course by Maximilian Schwarzmuller, but with a node/express backend and typescript and unit tests and with lerna

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

```
A Linux OS or MacOS (there are a few extra steps needed with Windows machines)
node version 12.7.0 or later
npm version 6.10.2 or later
PostgreSQL 13.0 with postgresql-contrib
```

### Installing

Clone GIT repository and download

```
git clone https://github.com/tomrembrown/QTCommunity
```

Update npm, node, and postgresql to latest versions and install postgresql-contrib. This project currently uses npm 6.11.0, node 12.9.0, PostgreSQL 11.5. These commands are for Linux:

```
sudo npm update -g npm
sudo npm install -g n
sudo n latest
echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main 11"
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt update && sudo apt-get install postgresql-11
sudo apt-get install postgresql-contrib
```

Build NPM script

```
npm install
```

Create environment file (copy either .env_prod or .env_dev)

```
cp .env_development .env
```

Determine port postgres runs on

```
sudo netstat -plunt |grep postgres
```

Build PostgreSQL initial database and add extension.

```
su - postgres (enter postgres user password)
psql --port (port determined for postgresql server)
CREATE DATABASE queer_toronto;
CREATE ROLE qt_computer_access WITH ENCRYPTED PASSWORD (enter password here);
GRANT ALL PRIVILEGES ON DATABASE queer_toronto TO qt_computer_access;
ALTER ROLE "qt_computer_access" WITH LOGIN;
CREATE EXTENSION IF NOT EXISTS citext WITH SCHEMA public;
\c queer_toronto
CREATE EXTENSION IF NOT EXISTS citext;
```

Adjust parameters in .env as necessary (such as postgres port and qt_computer_access password)

Create the database tables

```
npm run createDatabase
```

If using existing data, upload the latest data set

```
npm run uploadLatest
```

Increase the number of watches allowed for nodemon to work properly

```
echo fs.inotify.max_user_watches=582222 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

For development mode, start the server

```
npm run dev
```

In development mode, run webpack-dev server in browser at localhost:8080

For production mode, first build the bundles

```
npm run build
```

In production mode, run the node-express server at localhost:3000

```
npm run prod
```

## Running the tests

Tests are not currently configured

### What the tests do

These tests handle linting with jshint, link checking, and some cross-page and unit tests.

## Built With

- [Node.JS](https://nodejs.org/) - JavaScript runtime that allows server-side JavaScript
- [Express](https://expressjs.com/) - Backend framework
- [PostgreSQL 11](https://www.postgresql.org/) - Database
- [Vue.js](https://vuejs.org/) - Frontend framework

## Contributing

This is a proprietary project. Please ask Tom Brown (tom@tomrembrown.com) to add you to the private github repository in order to contribute.

## Authors

- **Tom Brown** - _Initial work_
- **David Yim** - _Access APIs to gather event data automatically_

See also the list of [contributors](https://github.com/tomrembrown/QTCommunity/contributors) who participated in this project.

## License

This project is proprietary - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

- Following along Ethan Brown's book 'Web Development with Node & Express' was useful
- Watching the NodeJS - The Complete Guide by Maximilian Schwarzmuller on udemy.com was helpful to upgrade the node and express to the latest ES2016 code.
- The series "You Don't Know JS" by Kyle Simpson was helpful to make sure the JavaScript was coded properly.
- Super sweet David Yim has provided much advice, support and encouragement :-)
