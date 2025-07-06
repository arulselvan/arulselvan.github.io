---
author: arul
category:
  - software-development
cover:
  alt: App-to-App-Deployment-Feature
  image: /wp-content/uploads/2017/08/App-to-App-Deployment-Feature.png
date: "2017-08-07T07:12:35+00:00"
guid: http://arulselvan.net/?p=324
tag:
  - nodejs
  - technical
title: How do manage environment based configuration node js/typescript
url: /manage-environment-based-configuration-node-jstypescript/

---
Any application needs configuration settings, the programming language like ASP.NET we typically use Web.config for configuration, for different environment we have separate files like

Web.Dev.Config,
Web.QA.Config,
Web.Staging.Config,
Web.Production.Config, etc.

In nodejs app I could not find any specific standard for this but there is a multiple option to setup this configurations, below I used .json file for different environment.

Folder Structure.
[![](/wp-content/uploads/2017/07/Screen-Shot-2017-07-10-at-3.09.52-PM-300x295.png)](/wp-content/uploads/2017/07/Screen-Shot-2017-07-10-at-3.09.52-PM.png)

default.json - this will hold all the base configuration and common to all the environment
Sample:

```
{
  "appName": "Sample Application",
  "cookieEnabled": true,
  "sessionEnabled": true
}

```

<environment>.json - for every environment there will be a separate  .json file, this contain configuration specific to that particular environment, this will override our base default values if same key exist.
Sample: development.json

```
{
  "db": {
    "connection": "mongodb://localhost:27017/sample_dev"
  }
}

```

**How its works?**
In the index.js we getting  configuration files using require and merging default and respecting environment file then doing export.

```
var defaults = require("./default.json");
var envConfig = require("./" + (process.env.NODE_ENV || "development")+".json");
export const config:any = Object.assign({}, defaults, envConfig);

```

process.env.NODE\_ENV is environment value, we can set on respective server, for testing I used npm script to set this value in my package.json

```
"scripts": {
    "start": "export NODE_ENV=production  && npm run build-server && npm run start-node",
    "build-server": "npm run copy-server-config && ntsc -p server",
    "copy-server-config": "copyfiles -u 1 ./server/config/**/*.json ./dist_serv",
    "start-node": "node dist_serv/server.js"
  },

```

Note: I tried with mac system, so setting environment value using "export NODE\_ENV=production", If you trying with windows may be need to change the command slightly like  "SET NODE\_ENV=production".

I used Typescript on the server, so during build copied all my configuration to deployment folder.

**Okay, how to access these configuration inside application?**

import the config and use wherever needs across the app, below snap  getting mongo db connection value using key "config.db.connection"

```
import * as Mongoose from "mongoose";
import { config } from "./../config";

export class DataAccess {
    static mongooseInstance: any;
    static mongooseConnection: Mongoose.Connection;

    constructor() {
        DataAccess.connect();
    }

    static connect(): Mongoose.Connection {

        if (this.mongooseInstance) return this.mongooseInstance;

        this.mongooseConnection = Mongoose.connection;
        this.mongooseConnection.once("open", () => {
            console.log("Connected mongodb.");
        });

        var dbConnection = config.db.connection;
        this.mongooseInstance = Mongoose.connect(dbConnection);

        return this.mongooseInstance;
    }
}

DataAccess.connect();

```

sample available on following path: [https://github.com/arulselvan/practice/tree/master/nodejs/environment-based-configuration](https://github.com/arulselvan/practice/tree/master/nodejs/environment-based-configuration)
