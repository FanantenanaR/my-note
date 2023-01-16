# Formidable
A Node.js module for parsing form data, especially file uploads.

## Installation
Execute the command bellow:
```cmd
npm install formidable --save
```

## Usage 
In service `service/upload.js`
```js
const fs = require('fs');

const initUpload = (file,targetPath)=>{
    console.log("upload init");
    return fs.promises.rename(file.filepath,targetPath)
        .then(()=>{ return "file uploaded"; })
        .catch((error)=>{
            console.error("error be ...............");
            throw error;
        });
};

module.exports  = {
    initUpload : initUpload
}
```

In configuration `config/upload-path.js`
```js
const fs = require('fs');

const initUpload = (file,targetPath)=>{
    console.log("upload init");
    return fs.promises.rename(file.filepath,targetPath)
        .then(()=>{ return "file uploaded"; })
        .catch((error)=>{
            console.error("error be ...............");
            throw error;
        });
};

module.exports  = {
    initUpload : initUpload
}
```

In Controller `controller/upload.js`
```js
const FORMIDABLE = require("formidable");

const {resourcePath : RESOURCE_DIR} = require("../../config/path-config");
const uploadService = require("../../src/services/upload");

const HttpStatus = {
    OK: { code: 200, message: 'OK' },
    CREATED: { code: 201, message: 'Created' },
    NO_CONTENT: { code: 204, message: 'No Content' },
    BAD_REQUEST: { code: 400, message: 'Bad Request' },
    UNAUTHORIZED: { code: 401, message: 'Unauthorized' },
    FORBIDDEN: { code: 403, message: 'Forbidden' },
    NOT_FOUND: { code: 404, message: 'Not Found' },
    INTERNAL_SERVER_ERROR: { code: 500, message: 'Internal Server Error' }
};

module.exports = {
    uploadFile : (req,res) => {
        const form = FORMIDABLE({multiples : false});
        form.parse(req,(err,fields,files)=>{
            if(err) throw err;
            const ext = files.sary.mimetype.slice(6);
            const fileName = `${RESOURCE_DIR}/${new Date().getTime()}.${ext}`;
            uploadService.initUpload(files.sary,fileName).then((content)=>{
                res.setHeader("content-type","text/plain");
                res.send(content);
            }).catch((error)=>{
                res.setHeader("content-type","text/plain");
                res.status(HttpStatus.INTERNAL_SERVER_ERROR.code).send(HttpStatus.INTERNAL_SERVER_ERROR.message);
            });
        });
    }
}
```

