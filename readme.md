## Next.js overview
---

[official-documentation](netxtjs.org/docs)

What is Next.js?
A React Framework

About Next.js
1. We still write code in react as we know it

2. Is it like create-react-app?
    - yes and no
        - yes in that they both make our life easier
        - No in that it enforces a strcuture so that we can do more advanced things like: 
            - Server Side Rendering
            - Automatic code splitting
3. Next.js has built in features where in create-react-app we would need to install
    - Routing 
    - head
    - hot code reloading
    - universal rendering

4. Static Exporting will export a react-less version of your code

5. Styles with CSS in JS


* I reccomend trying their geting-started tutorial when you have a moment as it is very good.
[getting-started](nextjs.org/learn/basics/getting-started)



## Server-Side Rendering with Next.js
---

1. ServerSide Rendering builds the page on the server-side and sends to the client
2. If you think how we have been doing api fetches with client side react
    - we request the api from the client ends for the data
3. Next js will do the first request from the server and send the data to the client, then more requests can be made from the client
4. Remeber the purpose of server-side rendering in react is to bridge the two. if we don't use server and client side rendering then why are we using react at all

## Why does it matter?
---

1. SEO and your sites content is much more scrapable when we use server side rendering to send over all the data
    - remember if we compare the SSR vs CLient the client has alot less HTML
    
2. If you someone has a bad internet connection or out of date device, SSR tends to be a better overall improvement but initial loading time can take longer
