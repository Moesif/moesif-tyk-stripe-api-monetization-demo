# moesif-Tyk-stripe-api-monetization-demo

This project was created to show a simple but end-to-end solution for monetizing APIs with Tyk, Stripe, and Moesif. 

For the full end-to-end configuration of this project, check out our [complete guide](https://www.moesif.com/blog/technical/stripe/tyk/End-To-End-API-Monetization-With-Tyk-Stripe-And-Moesif/)!

## Prerequisites
To run this project you must have __Node and npm installed__.

You must also have:
- an active instance of Tyk API gateway up and running with at least one API proxied through it
- Your endpoints in Tyk should be protected by __API Key__
- an active Stripe account with at least one __Product__ and __Price__ created
- Have an active __Stripe integration__ and __billing meter__ in Moesif which includes the endpoints you want to monetize. To set one up, check out our guide on it [here](https://www.moesif.com/docs/guides/guide-on-creating-a-billing-meter-with-stripe/).

## Installation

After you cloned your repo, in the root folder of the repo, to set up your environment and install dependencies, run `npm install`.

## Deployment

In the `.env` file, you will need to plug in a few details in order to make this work.

__STRIPE_KEY__ will contain the key to access the Stripe APIs.

__STRIPE_PRICE_KEY__ will contain the key to your Product's Price in Stripe

__MOESIF_APPLICATION_ID__ will contain your Moesif Application ID.

__TYK_AUTH_KEY__ This can be found in Tyk by navigating to the __Users__ page and clicking on a user's entry (likely your own).Once you’ve clicked on the user, you will be able to see the user's __Tyk Dashboard API Access Credentials__. This is the key you’ll plug into the config.

__TYK_API_ID__ The API ID for the endpoint can be found by going to the __APIs__ screen in Tyk and copying the __ID__ for your endpoint.

__TYK_API_NAME__ The __API Name__ for the endpoint. This can be found in the same place as the __API ID__.

__TYK_URL__ This will be the URL of the Tyk Dashboard API. Usually, this will be hosted on port 3000 but it may be different if you have a custom configuration.

To run the project, run `node app.js`. This will bring up the backend and frontend for the project.

The backend endpoint can be reached at http://localhost:5000/register. The frontend can be accessed through http://localhost:5000.

## How to use

In the frontend, you can add in an email, first name, and last name into the fields on the screen. Then click __Register__ to generate an API key.

IF you want to use the backend directly, you will need to create a request to the http://localhost:5000/register and include a JSON request body. It will look like this:

``` javascript
{
    email: "myemail@email.com",
    firstname: "firstname",
    lastname: "lastname",
}

```

Once sent, the response brought back from the __/register__ endpoint will contain an API key.

The API key can then be used to send requests to your __API key__ protected APIs in Tyk.

## Confirming the flow

Once you have registered a user using the __/register__ endpoint, you should see:

- A new API key created in Tyk under __Consumers__ which has the Stripe Customer_ID in the __Alias__ field.
- A new Customer in Stripe with the same Customer_ID you see in the __Alias__ field in your Tyk API key

Once you have sent a request to a protected API in Tyk, you should see the request in Moesif. The request should contain:

- The route information
- Stripe metadata (you'll need to inspect the request to see this)
- The User ID in Moesif will be the Stripe Customer_ID
- The Company ID in Moesif will be the Stripe Subscription_ID

Usage will be available in Stripe in a few hours. If data still isn't in Stripe after a few hours, reach out to Moesif support for help with your configuration.

## How to Contribute

For all changes and contributions we use the Github Pull request process as our workflow. Please see detailed instructions in notion on how to create branch and create pull requests.

https://www.notion.so/moesif/Github-Flow-583da5aaa9b54d118bea1dd4db17b97f

Most articles are written in markdown. Quick guide here: https://www.markdownguide.org/cheat-sheet/
