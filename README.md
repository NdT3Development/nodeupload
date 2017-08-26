# Node Upload
Decided to start from scratch using a different dependency for uploading. Basics are working yet this is **NOT** ready for use in a production environment.

### Installing
This project is not quite ready for public use yet, however, if you can use it if you want to.

```sh
npm install
node createUser.js # This is the script for creating users
node app.js
```

![InstructionsGIF](https://i.imgur.com/gMNDSZC.gif)

### Creating a New User
After you are done installing and your friend also want to use this, run the following command and answer the questions.

```sh
node createUser.js
```

### Usage

Once the server has started, open a web browser to `YOUR_IP:8099` (there will be an option to configure this at some time).

If everything worked, it should show an upload form. Just add your token where it says `Token`, choose a file to upload, then click the button. It should upload. If not, check the console for errors. You may need to open an issue here.

#### Admin Tools

There are also some admin tools (currently, deleting files and temporary files). These require an admin token which you get from answering `true` to the `Admin` question when running `createUser.js`.

You will need to use a program that can send headers with a GET request. I prefer using [Postman](https://getpostman.com).

 **Delete files in 'files' directory:**
  - Make a GET request to `YOUR_IP:8099/admin/deletefiles` including a header with your admin token with the name `admintoken`.

  **Delete files in temporary directory (`OPERATING_SYSTEM_TMP/nodeupload_tmp/`)**
  - Make a GET request to `YOUR_IP:8099/admin/deletetmp` including a header with your admin token with the name `admintoken`.


### KNOWN ISSUES
If you get an error like this after uploading, please manually create a directory called `nodeupload_tmp` in your operating system's tmp directory: ![Error1](https://i.imgur.com/TrdaOsK.png)

### Please note:
**THIS HAS NOT BEEN TESTED YET IN A PRODUCTION ENVIRONMENT. DATABASE FEATURES NOT FULLY TESTED. ALL DEVELOPMENT TESTS WERE RUN ON LINUX MINT 17.3 64 BIT USING NODE V8.4.0 AND NPM 5.3.0**

### LICENSE
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
