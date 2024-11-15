# constellette

## express path
Skip to the "HTTPWidget operation" section.

## prelude

The operation of HTTPWidget described below contains the structure of the
request and response from the RSWGame server. You can use these parameters
with any other tool that makes HTTP requests. See the list below.

## introduction
I like to know how many players have not yet submitted orders. If I've 
already sent in my orders, this number gives me a rough idea of when the 
next turn might run. If I haven't sent in my orders and the number 
reaches 1, I know the turn is waiting for me. There's no legal requirement
to finish the turn before the due date, but I like this motivation.

I thought about making an iPhone widget to show the game status. I might 
still make an app, but there are already apps that can display the information
in a widget.

## HTTPWidget operation

HTTPWidget is a free app that works on iOS, iPadOS, and MacOS. The app can make
a request to the RSWGame server, parse the response, and display
the result in a widget on your home screen. 

1. Get the app called HTTPWidget: https://apps.apple.com/us/app/httpwidget/id6447097633
2. Create a new widget and enter the following fields:
    * *in the HTTP BASIC section*
    * URL: https://rswgame.com/xml
    * HTTP Method: POST
    * Request Body: Raw
    * Raw Body:
    ```xml
    <?xml version='1.0'?>
    <request command='list'>
        <parameter keyword='accountId' value='YourAccountID' />
        <parameter keyword='password' value='YourPassword' />
        <parameter keyword='onlyMine' value='true' />
        <parameter keyword='format' value='xml' />
    </request>
    ```
    * *in the RESPONSE EXTRACT section*
    * Extract by: Regex
    * Regex String:
    ```
    gameID="YourGameID".*numWaitingFor="(\d+)"
    ```

Now press the *Send Request* button in the *RESPONSE* section. If everything
worked, the *Extracted:* line in the *RESPONSE EXTRACT* section should 
show the number of players yet to submit orders.

> include the basic example of the response so the regex makes sense,
and so that other tools might be used.

## other apps
There must be lots of apps that can make API calls and display the results.

#### requirements
* URL
* ability to parse XML result
* display result somewhere useful
* don't spam the server with simultaneous requests

#### platforms
* widgets? apps?
* MacOS?
* Android?
* Windows? 
* Linux?

