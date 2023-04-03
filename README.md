# CS3700 Project 5: Web Crawler
## Taiga Wad and Daniella Calle

## High Level Approach: 

We had a general procedure that we thought out and later implemented in code.

1. Send an intial ``GET`` request that retrieved the intitial page and looked for the CSRF Middleware token.

2. Send a ``POST`` request to log in using the credentials provided in args, using the ``sessionid`` and ``csrfmiddlewaretoken`` we extract in the first step.

3. Get the updated cookie after the ``POST`` request to use in future requests.

4. Start crawling, finding ``a`` tags and extracting their links to look through later, and looking for ``h2`` tags for possible flags.

5. Make sure to not look through old links.

6. For each flag we find, add to a list called ``flags`` that we eventually use later to see the flags.

This is pretty much what we followed to implement the protocol. We then proceeded to flesh out whateach step would look like, making sure that we were using the correct HTTP version, the cookies were what we expected, and the other fields were setup properly.

To extract the text in the tags and get the links, ***we used the HTML parsing functionality of BeautifulSoup***. The project description said we cannot use BeautifulSoup, but [on Piazza, Christo said we can](https://piazza.com/class/lcihjy4wpi06j6/post/521), so we used only the HTML parsing functionality of BeautifulSoup.


## Challenges: 
One of the challenges we faced was managing the Connection state. At first, our code took very long to run, with the final reception of the data taking upwards of a minute. This slowed down our code tremendously, and we spent a day or two stuck on just how to get it to receive all the information in a quicker way.

We asked some TA's, but it didn't seem to help, so we went to Piazza and asked for suggestions. Eventually, Christo answered and said we had to manage the ``Connection`` state dirctly in the HTTP request, closing the sockets there to make sure they actually close upon completing the request and sending the response. We implemented this the next day and were elated to see that our code ran much quicker.

It also took us a while to get the components of the cookie down right. We were using the wrong CSRF token to ``POST``, which meant we weren't logging in or crawling properly. 


## Testing: 

We did a lot of testing by using print statements to see what our GET and POST requests looked like, and also printed out the responses we were getting from the socket and verified that it was what we expected.

We also used the Developer Tools window on Fakebook to see what sort of requests we were sending and receiving as we progressed through the website. We used our observations to make sure the requests we made were accurate.

We then ran the crawler a few times to make sure we got the same flags each time.


