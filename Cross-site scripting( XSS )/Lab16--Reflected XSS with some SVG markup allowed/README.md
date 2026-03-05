# Lab-16: [Reflected XSS with some SVG markup allowed](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-some-svg-markup-allowed) 

This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some SVG tags and events. 

**Aim :-** To solve the lab, perform a cross-site scripting attack that calls the ``` alert() ``` function. 



## Solution
- Try searching with ``` <img src=1 onerror=alert(1)> ```, this returns **Tag is not allowed** error message.

- Open **burp suite** and intercept the search request with ``` <> ``` as search query an send it into **intruder**.

- Place the cursor between angle brackets and click **Add §** button to create payload position. ( The position will look like ``` <§§> ``` )

- Configure payload with all tags. ( Use tags from portswigger [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) )

- Start attack.

- In the responses most of the tags respond with **400** status code  except ```<svg> ```, ``` <animatetransform> ```, ``` <image> ``` and ``` <title> ``` responds with **200**. This confirms that these tags are allowed.

- Now replace the search query with ``` <svg><animatetransform%20=1> ``` and place the cursor before ``` = ``` character then click **Add §** button to create payload position. ( The search query will look like ``` <svg><animatetransform%20§§=1> ``` )

- Configure payload with all events. ( Use events from portswigger [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) )

- Start attack.

- In the responses most of the events respond with **400** status code except ``` onbegin ```. This confirms that ``` onbegin ``` event is allowed.

- Use ``` <svg><animatetransform onbegin=alert(1) attributeName=transform> ``` payload to search, this will popup with alert box with value 1.
