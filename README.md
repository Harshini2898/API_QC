# Sample - Group Consents Via Custom Consent API

This sample code illustrate an implementation of “Group Consents Via Custom Consent API.” Quantcast will not be providing support on this sample code, and is not responsible for any consequences of your implementation of this sample code.

This implementation allows you to share consent across multiple sites as documented in our "Group Consent Guide" (https://help.quantcast.com/hc/en-us/articles/360047737613). It will store the Choice cookies 'euconsent-v2', '_cmpRepromptHash', 'noniabvendorconsent' and 'addtl_consent' under the domain that you specify in the code as shown below.

## Installation
- Install node.js from the website https://nodejs.org/en/download/, this API was built
with the version 12.16.0 but you can use the latest 12.18.4

- Use the node package manager to install dependencies

```
npm install
```

## Usage

You will need to modify the code to adapt it to your site configuration.

Optional modifications:
- index.js: in the line 44 defines the path for the API. Change this to what you use in your environment.
 ```node
 server.use('/api/cmpV2', require('./routes/cookie'));
 ```
 Important: specify you domain name where you want to host this implementation:
 - cookieController.js: on the line 5 define your cookie domain
  ```node
 const cookieSettings = {
    domain: '.sample.com', // top level domain to set the cookies
	secure: true, // setting secure flag to false so we can test everything up on a local environment without the need to setup certificates
	sameSite: 'none', // setting the sameSite policies
	maxAge: 1000 * 180 * 24 * 60 * 60, // cookie max age in miliseconds
};
 ```

## Deployment

Configure the CMP for group consent using API (see https://help.quantcast.com/hc/en-us/articles/360047737613).
Deploy your implementation on the domain that you specified in cookieController.js.

Note: On browsers with strict ITP support (like Safari) you can share consent only between subdomains and its main domain. The API must be deployed under the main domain name.