# Nexmo PHP Skeleton Application

This is a basic Slim 4 PHP application to test and debug your Nexmo credentials and environment. Utilize this application to test that your API credentials are in working order and to examine the event webhook data you receive when API requests are received by Nexmo from your account.

* [Requirements](#requirements)
* [Installation and Usage](#installation-and-usage)
  * [API Credentials](#api-credentials)
  * [Using ngrok](#using-ngrok)
  * [Running the Application](#running-the-application)
* [Contributing](#contributing)
* [License](#license)

## Requirements

This application requires that you have the following installed locally:

* [PHP 7.1 or higher](https://www.php.net/)
* [Composer](https://getcomposer.org/)
* [Nexmo PHP Server SDK](https://packagist.org/packages/nexmo/client)

Additionally, in order to test your Nexmo account, you must have a Nexmo account. You can create a Nexmo account for free or manage your Nexmo account details at the [Nexmo Dashboard](https://dashboard.nexmo.com).

This application is meant to be run as a standalone test, but it can also be used with a web server like Apache or nginx.

## Installation and Usage

You can run this application by first cloning this repository locally:

```bash
composer create-project nexmo/php-skeleton-app
```

Alternatively, you could clone this repository through git

```bash
git clone git@github.com:Nexmo/php-skeleton-app.git
```

Once you have downloaded a local copy, change into the directory of the application in your terminal. You can now set up the application for your Nexmo account.

### API Credentials

In order to test your API credentials, rename the provided `.env.sample` file to `.env` and supply the values for the following environment variable keys:

* NEXMO_API_KEY=
* NEXMO_API_SECRET=

The `NEXMO_API_KEY` and `NEXMO_API_SECRET` are to be provided with your API key and secret, respectively. 

As always, make sure to not commit your sensitive API credential data to any public version control. 

### Using ngrok

In order to test the incoming webhook data from Nexmo, the Nexmo API needs an externally accessible URL to send that data to. A commonly used service for development and testing is ngrok. The service will provide you with an externally available web address that creates a secure tunnel to your local environment. The [Nexmo Developer Platform](https://developer.nexmo.com/concepts/guides/testing-with-ngrok) has a guide to getting started with testing with ngrok. 

Once you have your ngrok URL, you can enter your [Nexmo Dashboard](https://dashboard.nexmo.com) and supply it as the `EVENT URL` for any Nexmo service that sends event data via a webhook. A good test case is creating a Voice application and providing the ngrok URL in the following format as the event url: 

`#{ngrok URL}/webhooks/event`

You can then call your Nexmo Voice application, and with your skeleton application running you can observe the webhook data be received in real time for diagnosis of any issues and testing of your Nexmo account.

### Running the Application

Once you have your API credentials incorporated and your ngrok setup ready, you can go ahead and use this skeleton app. To start the application's server, run the following from the command line inside the directory of the app:

```bash
composer run --timeout=0 serve
```

You can test that your credentials work by sending a test SMS by navigating to `https://localhost:8000/` in your browser, and fill out the form. You will need to supply:

1. A number to send the SMS to, such as your personal mobile phone
2. A number you wish the test SMS message to originate from. For example, this could be your [Nexmo provisioned virtual phone number](https://developer.nexmo.com/numbers/overview)
3. A message to send

The skeleton app is also capable of receiving Nexmo API webhook data. As mentioned in the [Using ngrok](#using-ngrok) section above, a good candidate for that test is a Nexmo Voice application. From within your Nexmo dashboard you can create a Nexmo Voice application, provision a Nexmo virtual phone number and then link that number to your Voice application. Once you have ensured that your new Voice application's `EVENT URL` is `#{ngrok URL}/webhooks/event`, you can then give your Nexmo number a phone call. You should see the webhook data in your console in real time. For example, data for a ringing phone call will look like this:

```
[Mon Mar 16 22:03:24 2020] {"from":"447700900000", "to":"447700900000", "uuid":"a123456789012345fbdsw", "conversation_uuid":"CON-234567-fdsfs34-vfddfh-btger3-22345", "status":"ringing", "direction":"inbound", "timestamp":"2020-01-07T11:24:49.478Z"}
```

You can exit your application at anytime by holding down the CTRL and C keys on your keyboard.

## Contributing

We ❤️ contributions from everyone! [Bug reports](https://github.com/Nexmo/php-skeleton-app/issues), [bug fixes](https://github.com/Nexmo/php-skeleton-app/pulls) and feedback on the application is always appreciated. Look at the [Contributor Guidelines](https://github.com/Nexmo/php-skeleton-app/blob/master/CONTRIBUTING.md) for more information and please follow the [GitHub Flow](https://guides.github.com/introduction/flow/index.html).

## License

This projet is under the [MIT License](LICENSE.md)
