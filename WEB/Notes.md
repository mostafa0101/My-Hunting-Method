#### CSR (Client-Side Rendering) & SSR (Server-Side R) & SSG (Static-Side Gen)
    - CSR is good for very interactive apps, like web games.
    - SSR is good for websites with content that changes a lot, like news sites.
    - SSG is good for static websites, like blogs and company sites.

#### Caching
    - Cache is temporary storage that saves data to help websites load faster when you revisit them 
    - CDN's (Content Delivery Network) stores copies of your website on servers around the world, when a user make a request it response with colsest server to him
   
    - Types of Cache storing 
        1- Client-side (local on the user device)
        2- Server-side (the server store a request that made many times by many users)

    - Cache keys to compare the request with the saved one by creating a unique fingerprint for each request if it match it send the saved response if it's not it send it to the server to get new response

    - Possible Bugs (Cache Deception and Cache Poisoning)

#### DOM (Document Object Model)
    - Sources are the places where the user input enters the app
        - location.[href-search-hash]
        - document.[URL-referrer]
        - localStorage , sessionStorage , cookies

    - Sinks the place where the user input executed
        - innerHtml , outerHtml , document.write() , eval() , setAttribute() , window.location [for redirect]

#### Origin Policy
    - SOP Security header protect user data from other websites 
    - COP (Cross Origin Policy) happens between server to server without the need of your data
    - Simple Request use methods like GET POST and limited to specfic content type
    - Preflight Request is an additional HTTP request that a web browser sends to the server before making a cross-origin AJAX request, the browser automatically sends an HTTP OPTIONS request to the server before the actual request


#### Ajax
    - Ajax a tech used to update parts of webpage without refreshing it

#### XHR (XMLHttpRequest)
    - tool or object in JS allows to send http/s request whith the server and get response/data back without reloading the page (any type of data)

#### Fetching API
    - same as the XHR but more simpler it's also an AJAX 
    - fetch('user.json') & catch()
    
#### postMessage
    - 


#### load balancers
    - Distribute requests to different servers to avoid overwhelming

#### Reverse Proxy Servers
    - Sit between client & server to manage traffic efficienty (ex: Nginx & Apache) 

#### Content Discovery Networks (CDNs)
    - Enhance the user experience by enhance the speed of the internet 
    - Simply when the user ask for data it deliver the data from the closest source 

#### 





    
