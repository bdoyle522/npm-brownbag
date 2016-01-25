# Create and publish NPM pkgs

### Directory Structure

```
/projectName
  -- /src
     -- /bin
        -- uppercaseme
     -- /lib
        -- uppercaseme.js
     -- package.json
     -- README.md
  -- myfile.txt          
```

---

### myfile.txt

```
lorem ipsum dolor sit amet, consectetur adipiscing elit. donec a diam lectus. sed sit amet ipsum mauris. maecenas congue ligula ac quam viverra nec consectetur ante hendrerit. donec et mollis dolor. praesent et diam eget libero egestas mattis sit amet vitae augue. nam tincidunt congue enim, ut porta lorem lacinia consectetur. donec ut libero sed arcu vehicula ultricies a non tortor. lorem ipsum dolor sit amet, consectetur adipiscing elit. aenean ut gravida lorem. ut turpis felis, pulvinar a semper sed, adipiscing id dolor. pellentesque auctor nisi id magna consequat sagittis. curabitur dapibus enim sit amet elit pharetra tincidunt feugiat nisl imperdiet. ut convallis libero in urna ultrices accumsan. donec sed odio eros. donec viverra mi quis quam pulvinar at malesuada arcu rhoncus. cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. in rutrum accumsan ultricies. mauris vitae nisi at sem facilisis semper ac in est.
```

---

### /lib/uppercaseme.js

```   
"use strict"
var fs = require('fs');

function convertThis() {
    if(process.argv.length > 2) {
        var myfile = process.argv[2];

        if(fs.existsSync(myfile)) {
            var content = fs.readFileSync(myfile, 'utf8');
            fs.writeFileSync(myfile, content.toUpperCase());
            console.log("Done");
        } else {
            console.log("File does not exist - " + myfile);
        }
    } else {
        console.log("Pass on a file name/path");
    }
}

exports.convert = convertThis;
```

---

### /bin/uppercaseme

```
   
#!/usr/bin/env node

"use strict";
var path = require('path');
var fs = require('fs');
var lib = path.join(path.dirname(fs.realpathSync(__filename)), '../lib');

require(lib+'/uppercaseme.js').convert();
```

---

### Test

```
node ./src/bin/uppercaseme ./myfile.txt
```

---

### /src/package.json

```
{
  "author": "devloper",
  "name": "uppercaseme0001",
  "description": "Converts files to uppercase",
  "version": "0.1.1",
  "repository": {
    "url": ""
  },
  "main": "./lib/uppercaseme",
  "keywords": [
    "upper",
    "case",
    "file"
  ],
  "bin": {
    "uppercaseme": "./bin/uppercaseme"
  },
  "dependencies": {},
  "engines": {
    "node": "*"
  }
}
```

---

### /src/README.md

Must contain a README.md otherwise npm will throw an error

---

### Link

```
npm link (may need to sudo)
```

### Create user

Before publishing to the NPM registry:

```
npm adduser
Username:
Password:
Email:
```

---

### Publish

Publishing is done in the same directory where the package.json resides.

```
cd src
npm publish
```

---

The console, should display:

```
npm http PUT https://registry.npmjs.org/uppercaseme
npm http 201 https://registry.npmjs.org/uppercaseme
npm http GET https://registry.npmjs.org/uppercaseme
npm http 200 https://registry.npmjs.org/uppercaseme
npm http PUT https://registry.npmjs.org/uppercaseme/-/uppercaseme-0.1.1.tgz/-rev/1-74d3bb0b59747a421
5b7b3778dcc02c0
npm http 201 https://registry.npmjs.org/uppercaseme/-/uppercaseme-0.1.1.tgz/-rev/1-74d3bb0b59747a421
5b7b3778dcc02c0
npm http PUT https://registry.npmjs.org/uppercaseme/0.1.1/-tag/latest
npm http 201 https://registry.npmjs.org/uppercaseme/0.1.1/-tag/latest
+ uppercaseme@0.1.1
```

---

### Installation and Usage:

In a different directory:

```
mkdir upprTester
cd upperTester
npm install uppercaseme
echo "hello world" > myfile.txt
```

---

Then to convert

```
./node_modules/.bin/uppercaseme myfile.txt

or

"./node_modules/.bin/uppercaseme" myfile.txt
```

---

### Global

First remove old package

```
npm uninstall uppercaseme
npm install -g uppercaseme (may need to sudo)
```

---

### Run it

```
uppercaseme myfile.txt
```
