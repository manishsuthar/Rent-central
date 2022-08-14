This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify

### Temporary Bucket Details

Success! Your new application key has been created. It will only appear here once.
keyID: 001566b9670231a0000000002
keyName: testing-om-bucket
S3 Endpoint: s3.us-west-001.backblazeb2.com
applicationKey: K001bxMORI7SvIX0Bsa2JCtemohrGco

## How to use Logger

Format [LEVEL][date][Class][path:line]
LOG LEVELS = INFO:info | DEBUG:debug | ERROR:error | WARN:warn

- To Use Logger you need import class logger like
  1. const log = require("../logger/Logger")(CLASSNAME);
  2. log.[LEVEL](INFOMATION);
     log.info(ANY);
     log.error(ANY);
     log.warn(ANY);
     log.debug(ANY);
  3. Log files are available at .
     - on Linux: ~/.config/s3-sync/logs/main.log
     - on macOS: ~/Library/Logs/s3-sync/main.log
     - on Windows: %USERPROFILE%\AppData\Roaming\s3-sync\logs\main.log
  - Log file size 5 MB

## Amazon Store Util Methods

| Fucntion          | Summary                                        | API                                                             |
| :---------------- | :--------------------------------------------- | :-------------------------------------------------------------- |
| listBuckets       |                                                | API                                                             |
| isFolder          | ....                                           |                                                                 |
| isFile            | ....                                           |                                                                 |
| size              | ....                                           |                                                                 |
| getObjectMetadata | ....                                           | Response object: {file:true/false, size:bytes, etc metadata...} |
| setObjectMetadata | Can be used to set the metadata on the object. | Response object: {file:true/false, size:bytes, etc metadata...} |

## Progess Plan

## Framework

Listing the buckets:  
Responsibility is listing buckets:

- Every request could have identifier. it can be string, but it unique identifies the request. For example: ['REFRESH_FROM_LST_BUCKET']
- Logging framework.

  - Log levels
  - Log to file and console both.
  - Log rotation.
  - Log formatting. We should be able to format our way.
  - Log class or method name.

- It should take a listingRequest <= AbstractRequest.
- It should return s listingResponse <= AbstractResponse
- All the promises will throw the error. So, that await can be used and every called has to wrap them around try catch. or put catch on the promise.
- Then add test case for each util method. And make sure test case is running.

## Storage Framework

1. AbstractStorage
1. list('/'); => if this on amazon, it will internall call list buckets. list("s3:///) => then also return list of buckets. list("s3:///abc) => Returns the contents of abc.
1. copy(source, destination); storage.copy(sourceStorage, "file:///url/ab/c/" , "file:///a/b/c") <=
1. AmazonStorage.js <= extends from AbstractStorage.
1. FileSystemStorage.js <= extends from AbstractStorage.

## Pending For Future

1. Implement alpha numberic sort.
2. Test with directories which have more that 10000 files.
3. Test with directories which have more that 10000 on s3.
4. Backblaze paths or s3 needs to URL encoded.
