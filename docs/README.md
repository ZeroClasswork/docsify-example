# API Calls

## Introduction

The Petfinder API ([Application Programming Interface](https://en.wikipedia.org/wiki/API)) allows you to access the Petfinder database of hundreds of thousands of pets ready for adoption and over ten thousand animal welfare organizations. You can use the API to build your own dynamic websites or applications backed by the same data used on Petfinder.com.

### Capabilities

With the Petfinder API, you can:

- Search for and display pet listings based on pet characteristics, location, and status.
- Search for and display animal welfare organizations based on organization name, ID, and location.

You can, for example, display a random selection of available pets on a webpage; set up pages to display pets in various categories; allow visitors to your site to search for adoptable pets based on a number of criteria; or display profiles of local organizations.

### Using the API

This is a [RESTful](https://en.wikipedia.org/wiki/Representational_State_Transfer) API, meaning that it uses predictable URLs to access resources and, in case of an error, returns meaningful HTTP response codes. This enables the use of GET, POST, and HTTP authentication, which standard HTTP clients understand. The API supports [cross-origin resource sharing](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which allows you to use it securely from a client-side web application. You use the API by sending requests with a specific structure to our servers. In order to maintain security, it uses access tokens for API requests.

#### Getting Authenticated

The Petfinder API uses [OAuth](https://en.wikipedia.org/wiki/OAuth) for secure authentication.

In order to begin, you need:

- A Petfinder account; if you do not have one, [create an account](https://www.petfinder.com/user/register/).
- A Petfinder API Key (otherwise called Client ID) and Secret. (Visit [www.petfinder.com/developers](www.petfinder.com/developers) to request one.)
- A way of sending requests to our server along with information that will tell it you are allowed to do so. We recommend [cURL](https://en.wikipedia.org/wiki/CURL) for testing.

Once you have your API Key and your Secret, you can use these to request an access token. This token will enable you to receive information from our servers.

To get a token, make the following request, replacing {CLIENT-ID} and {CLIENT-SECRET} with your own information:'

```
curl -d "grant_type=client_credentials&client_id={CLIENT-ID}&client_secret={CLIENT-SECRET}" https://api.petfinder.com/v2/oauth2/token
```

The server will send back a response in this format:

```
{
  "token_type": "Bearer",
  "expires_in": 3600,
  "access_token": "..."
}
```

Breaking this down:

- The "token_type" value of "Bearer" means the server will not expect other identification along with the token; it is sufficient alone.
- The "expires_in" gives the time in seconds the token may be used; after this, your system must request a new one and use that.
- The "access_token" is the token itself. You’ll need to have your system store this as a variable and include it in the header of every API request until it expires and you request another.