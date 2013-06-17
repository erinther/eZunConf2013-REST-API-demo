# eZ Publish REST API Demo

This repository contains a very rough example of the usage of the REST API in
JavaScript presented at [the eZ Unconf #2 in
2013](http://share.ez.no/blogs/ez/ez-unconference-2-look-back-at-the-event-slides-and-pics).

The application allows to take a picture with the webcam of the computer and to
create the corresponding Image content in the eZ Publish repository with the
REST API!

## Requirements

  * a recent eZ Publish 5 install (5.1 or 2013.04, might also work with an earlier
    versions)
  * a modern browser [supporting getUserMedia/stream
    API](http://caniuse.com/stream)
  * a computer with a webcam

## Install

  * Clone this git repository
  * Copy or symlink the `demorest` folder to make it accessible via your web server BUT outside 
    you eZ Publish installation
  * Make sure your have different hostnames. This example could be on http://localhost/demorest/
    and the eZPublish on something different like http://ezdemo.local
  * Edit line 112 
    ``` resource = 'http://ezdemo.local' + resource; ```
    and change the host name if yours is different than http://ezdemo.local
  * Edit the line 116
    ```
    request.setRequestHeader( 'Authorization', 'Basic ' + Base64.encode( 'user:password' ) );
    ```
   and replace 'user:password' with valid values for you eZ Publish installation
  * copy the `.htaccess_for_ezp_web` file into your eZ Publish `web` folder and rename it to `.htaccess`.
    This file is meant to solve the [CORS](https://developer.mozilla.org/en-US/docs/HTTP/Access_control_CORS) requirements.
    If you have your `demorest` placed on a different domain than localhost edit first line of `.htaccess` 
    and put correct domain there.
  * make sure you have the `headers` apache2 module installed otherwise you will get 500 errors
    when you will try yo access your eZ Publish site
  
## Usage

  * Go to http://[ezpublish-url]/demorest/
  * The browser should ask for the permission to use the webcam
  * Click on *Capture!* to take a picture with your webcam
  * In *Your profile* part, fill a name and click on *Publish*
  * The first time you click on *Publish*, the browser should ask for a login
    and a password of an eZ Publish user with the permission to create content
  * The log part in the right should fill itself with messages and at the end of
    the publish operation, a link to the newly created content should be
    available

Here are the results in one screenshot:

![Screenshot of the app](https://github.com/ezunconference/eZunConf2013-REST-API-demo/raw/master/screenshot.png)

[A screencast is also available in REST API Demo application at the eZ Unconf](
http://share.ez.no/blogs/damien-pobel/rest-api-demo-application-at-the-ez-unconf-2)
blog post on share.ez.no ([A french version of this post is also
online](http://damien.pobel.fr/post/ez-publish-rest-api-v2-demo-unconf-2013)).

## Session authentication

Since eZ Publish 5.1, it's also possible to create a session through the REST
API. The code to test this new feature is embed in the demo, but not activated.

Here are the steps to use this new feature:

  1. Close and open again your browser so that it *forgets* the basic auth
  1. Remove the cookies for the domain your are working on
  1. [enable the session authentication in eZ
     Publish](https://confluence.ez.no/display/EZP/REST+API+Authentication#RESTAPIAuthentication-Settingitup)
  1. Unhide the login form by commenting the `display: none` CSS rule in
     style.css (around line 50)
  1. Uncomment the two `//,'X-CSRF-Token': tokenEl.innerHTML` lines (Warning:
     make sure to keep the comma at the beginning of those lines)

The first time you want to create an image, you now need to click on the
*Login!* button to authenticate your self. The rest of the usage paragraph
remains the same.
