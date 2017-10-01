# NodeUpload
###### (Yeah, not the best name but I can't think of good names)
Decided to start from scratch using a different dependency for uploading. Basics are working and I think it is ready for running in a production environment.

**All screenshots use the tokens from the first GIF under the installing section. The screenshots may not be up to date so don't worry if the output in console looks slightly different.**

## Installing
Should be easy to install and use

You will need Git and Node **v8+**

```sh
npm install
node createUser.js # This is the script for creating users
nano config.json # If you want to change the default settings (you can use something other than nano for this)
node app.js
```

![InstructionsGIF](https://i.imgur.com/gMNDSZC.gif)

## Creating a New User
After you are done installing and your friends also wants to use this, run the following command and answer the questions.

```sh
node createUser.js
```

## Usage

If the server is not already started, run `node app.js`.
Once the server has started, open a web browser to `YOUR_IP:PORT` (where `PORT` is the port specified in the config file (`config.json`)).

If everything worked, it should show an upload form (unless disabled in the config file). Just add your token where it says `Token`, choose a file to upload, then click the button. It should upload. If not, check the console for errors. You may need to open an issue here.

![UsageGIF](https://i.imgur.com/bZqbH0t.png)

Some file extensions are blacklisted by default. These can be changed in the config file.
- .exe
- .html
- .htm
- .bat
- .cmd
- .sh

### Admin Tools

There are also some admin tools (currently, deleting files and temporary files). These require an admin token which you get from answering `true` to the `Admin` question when running `createUser.js`.

You will need to use a program that can send headers with a GET request. I prefer using [Postman](https://getpostman.com).

 **Delete files in 'files' directory:**
  - Make a GET request to `YOUR_IP:PORT/admin/deletefiles` including a header with your admin token with the name `admintoken`.

  ![DeleteFiles](https://i.imgur.com/aVtL3d7.png)

  **Delete files in temporary directory (`OPERATING_SYSTEM_TMP/nodeupload_tmp/`)**
  - Make a GET request to `YOUR_IP:PORT/admin/deletetmp` including a header with your admin token with the name `admintoken`.

  ![DeleteTMP](https://i.imgur.com/XXUjU38.png)

## FAQs

  > What is this?

  NodeUpload is a Node.js server application that lets you run your own private file upload service. It uses randomly generated tokens for upload authentication and includes some admin features that require an admin token (which are generated when running  `createUser.js` and answering `true` to the `Admin` question).

  > How are uploads done?

  When a user uploads a file, it will be stored in a directory in your operating system's temp directory. Then there will be a connection to the database to check that the token is valid. If it is valid, the file gets moved to the `files` directory in the app's directory.

  > How are tokens generated?

  Tokens generated are **not** based on any information given when running `createUser.js`. The information there is only used to be stored in the database. The token is generated by the [`uuid` module](https://www.npmjs.com/package/uuid) (`uuid/v4`) to generate a completely random token.

  > What is the difference between a token and an admin token?

  A token (or upload token) is used for uploading files where an admin token is used for things like deleting files. An admin token cannot be used to upload and an upload token cannot be used for admin actions.

  > Why can a user with an admin token still do admin actions after their token has been disabled.

  Currently there is not a check for enabled accounts when doing admin actions. Uploads for disabled accounts will still be blocked however admin actions won't.

  > Does it check for information already existing in the database when running `createUser.js`?

  Yes, this feature has been added.

  > Is there any way to change the port that it runs on?

  To change the port that NodeUpload runs on, edit the config file (`config.json`).

  > Is there any way to change the length of the generated file names of uploads?

  To change the length of the auto generated file names of uploads, edit the config file (`config.json`).

  > Is there any way to change the responses (console output, web responses, etc.)?

  Yes, there is. Edit the `strings.json` file. The placeholders (`{{placeholder}}`) in these cannot be used in all strings. The code will have to be changed if you want to add these into strings that do not have support for it. More info coming soon.

  > Can I contribute to the development of NodeUpload by opening pull requests?

  Yes, you can open a pull request but please use the format [here](https://github.com/NdT3Development/nodeupload/blob/master/PULL_REQUESTS.md)

  > I found a bug, how do I report it?

  To report a bug, open an issue using the format [here](https://github.com/NdT3Development/nodeupload/blob/master/BUGS.md)

  > Can I request a feature?

  Yes, I am open to feedback and feature requests. Just open an issue using the format [here](https://github.com/NdT3Development/nodeupload/blob/master/FEATURE_REQUESTS.md)

  > Why was NodeUpload only 'production ready' in version 4.0.0?

  Decided not to use v0.x.x as the development version numbers as NodeUpload was probably production ready with a few changes to the code. Other reason: I don't actually know why I did it like this... ¯\\\_(ツ)\_/¯

  > Console full of errors... How do I get this working?

  Go to the [`Errors and Solutions`](#errors-and-solutions) section below

## Errors and Solutions
You may come across some of these while using this.

- `EACCES` (Permission denied): Make sure that you have permissions to access files in that directory.

- `EADDRINUSE` (Address already in use):
![NodeEADDRINUSE](https://i.imgur.com/gjOM9Vp.png)

  Make sure that there is no application running that is using that port. If you don't know what process is using the port, run the following **(LINUX ONLY)** `netstat -peanut | grep 'PORT_HERE'` then run `kill 'PROCESS_ID'` (The process ID will be in a format like `12345/process`)

  ![KillProcess](https://i.imgur.com/zlgFpew.png)

- `ENOENT` (No such file or directory):
![NoNodeUploadTMP](https://i.imgur.com/lxe00fe.png)

  You should not find this as NodeUpload should automatically create a new temporary directory if none is found. However, if you do find this issue, make a new directory named `nodeupload_tmp` in your operating system's temporary file directory. (If the error says it is missing the temporary directory.)

- `ENOENT` after installing dependencies: You may see an error that looks like this after installing the dependencies:
![SQLiteENOENT](https://i.imgur.com/bhJ7BbG.png)

  To fix this, delete the `node_modules` directory and run `npm install` again.

- `The program 'node' is currently not installed.`
![NodeNotInstall](https://i.imgur.com/xUHT8FJ.png)

  Follow the instructions [here](https://nodejs.org/en/download/package-manager/)

- `The program 'npm' is currently not installed.`

  Same as above.

- `Error: Cannot find module`

  ![NodeModule](https://i.imgur.com/YjtkIqQ.png)

    Run `npm install` in the terminal

  **For other errors, search for the error online or open an issue**

## LICENSE
MIT License

Copyright (c) 2017 NdT3Development

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
