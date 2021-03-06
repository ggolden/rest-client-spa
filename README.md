# rest-client-spa
Example REST client as a Single Page Webapp (SPA) using AngularJS

Inspired by the [Nutshell Developer Take Home Project](https://github.com/nutshellcrm/join-the-team/blob/master/developer-questions.md#rest-api-client) 

This sample shows how a webapp can get data from a REST API on a server.  It uses:
- HTML5 - the language of browsers
- Javascript - the other language of browsers
- Angular JS - a Javascript framework
- Moment JS - to handle dates in Javascript
- Bootstrap - a CSS framework to make things pretty

and connects to Nutshell's sample REST API.

### To Run

1. Download the client.html file from GitHub to your local computer.
2. Open the downloaded client.html in a browser that is not blocking CORS (see below), such as Safari on OSX

### Tricky Bits

#### [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)

Under ideal circumstances, this would run in any browser.  But browsers have security, and for the most part block any attempt to access REST APIs on servers that are not in the same domain as the source of the web page.  Usually, our web page(s) and server API(s) are in the same domain, so this is not a problem.  But for this sample, the web page is local, and the API is on Nutshell's domain.

Most browsers will generate a CORS exception and block the server call.  For example, running in Firefox:

`Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at http://join.nutshell.com/people/1. (Reason: CORS header ‘Access-Control-Allow-Origin’ missing).  (unknown)`

Safari on OSX will allow cross-origin REST calls, if the .html file is run from the local file system.

Nutshell could make this a bit easier to use if they added a header to the response from the REST API:

`Access-Control-Allow-Origin: *`

Although this solution may require fielding not only GET but OPTION requests on the server.

#### Dates

Part of the stated problem involves sorting by date, and Nutshell made it challenging by using a date format that is a little inconsistent and doesn't sort as text.

We need to parse these into Javascript Date objects, then do proper sort by the date values.  Moment.js is a great package to handle dates, and can easily parse this format.

#### Code Structure

For a commercial product, I would usually use separate files for the HTML, CSS, and a few for the Javascript.  I would also serve any third party dependencies (Angular, Moment, Bootstrap) from copies on our servers, so we are not dependent on the availability and performance of a content delivery network (CDN) for our product.

For this sample, it's all in a single file, and we reference our dependencies from public CDNs.
