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

## To Run

Under ideal circumstances, this would run in any browser.  But...

Browsers implement security, and for the most part block any attempt to access REST APIs on servers that are not in the same domain as the source of the web page.
Usually, this works out fine, since usually, the web page(s) and server API(s) would be in the same domain.  But in this case, the web page is either local or being served right from
GitHub, and the API is on Nutshell's domain.

Most browsers will generate a CORS exception and block the server call.  For example, running in Firefox:

`Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at http://join.nutshell.com/people/1. (Reason: CORS header ‘Access-Control-Allow-Origin’ missing).  (unknown)`

It turns out that Safari on OSX runs this, not caring about CORS in this case.

## Tricky Bits


#### Dates

Part of the stated problem involves sorting by date, and Nutshell made it challenging by using a date format that is a little inconsistent and doesn't sort as text.

We need to parse these into Javascript Date objects, then do proper sort by the date values.  Moment.js is a great package to handle dates, and can easily parse this format.

#### Code Structure

For a commercial product, I would usually use separate files for the HTML, CSS, and a few for the Javascript.
I would also serve any third party dependencies (Angular, Moment, Bootstrap) from copies on our servers, so we are not dependent on the availability and performance of
a content delivery network (CDN) for our product.

For this sample, it's all in a single file, and we reference our dependencies from public CDNs.
