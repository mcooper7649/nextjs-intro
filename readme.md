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



## Intalling Next.js
---

1. Next.js is an npm package that will need to be installed wherever we want to use it
    - normally we would create a directory first
    - then we npm init -y to intialize our npm package with yes as default values
    - npm install --save react react-dom next

2. Navigate to your package.json first and find the scripts object
    - inside we want to add "dev": "next"
    - this enables npm run dev 
    - inside the scripts object add "build": "next build"
    - this we wont use but is needed for production builds
    - inside the scripts object add "start": "next start"
    - this starts the server
3. npm run dev what we will use for our development purposes
    - if we run it now, we will get an error
        - "Couldn't find a pages directory. Please create one under the project root"
        - we need to create a pages directory in the root
4. npm run dev from the terminal and go to localhost:300
    - if configured correctly, we should receive "404 this page can not be found."


## Coding our pages
---

index.js

- Inside our pages directory, lets create index.js
- In the below example you can see we are returning  an h1 and export our function 
Index
- Remember the file needs to be named index, the function can have any name
- YOU MUST export default then the namae, if you try to export {index} you will get errors

```
const Index = () => {
   return (
    <div>
        <h1>Our Index Page!!!</h1>
    </div>)
}

export default Index;
```

## Pages Directory Details
--

1. The pages directory is where you can add pages like our index.js page. We can add components or an src folder if you like, as sometimes we don't need to create a page



## Next.js Routes
---

1. If you duplicate the index.js and make it a contact.js and go to the page you will see it renders.

2. This means Next.js has routing built-in

3. notice that when you access the page, the routing loads the page instead of laoding on the client side like a single page app.
    - WE can add this funcitonality!

4. If you were to console.log something from next.js on the index.js page for example it would log it on the node side of things AS well as going to the client side of things after

5. Basics of routing
    - Create pages folder
    - creation of pages inside this folder automatically generate a corresponding route

## Linking and Client Side Routing in Next.js
---

1. We want to make single page apps. How do we get rid of the page loading on route change?
    - Link is what wew can use for this, similar to React
    - import Link form "next/link";
    - inside our index we can add the link tag like below
        - ``<Link href='/=about'><a>About Page</a></Link>``
        - the anchor link is needed and no href!
2. How to create a button or div or span within our ``<Link>`` tags?
    - First lets examine the anchor tag we added to understand what we can add. Inside the react developer tools we can inspect the anchor and see an onClick is added to the anchor to make the routing work. 
    - We can add any element that supports an onClick, Ill add a button for this example.
    
        
## Components with Next.js
--

How do we use components instead of making a whole page?

1. So if we wanted to create a Navbar Component that will be on all our pages. We dont actually need to create it in our '/pages/' directory. We can create a components folder and link from the pages to use a component. As long as you are linking to a page thats in the pages directory it the component can work.

2. This also means we can take our routes and put them inside the Navbar component instead of the index.js like our example below. View the example below of our Navbar component.

```
const Navbar = () => {
    const styles = {
        display: "flex",
        background: "grey",
        justifyCOntent: "spacce-between",
        padding: "1rem"
    };
    return (
        <div style={styles}>
            <Link href='/'>
                <a>Home Page</a>
            </Link>
            <Link href='contact>
                <a>Contact Page</a>
            </Link>
            <Link href='/about'>
                <a>About Page</a>
            </Link>
        </div>

    )
}

export default navbar
```

4. Lastly we just need to add the Navbar to each page
    - import '../components/navbar.js'
    - use a div or fragment to wrap our code
    - add the navbar




## Another Option!! _app.js
--

1. This can overide page content! wait what?
    - Next.js uses the 'App' component to initialize pages
    - You can override it and contorl the page initialization
    - Which allow you to do things link
        - Persiting Layout between page changes
        - keeping sate when navigating pages
        - custom error handling using componentDidCatch
        - Inject additional data(for example by processing GraphQL)

2. To override, create the './pages/_app.js' file and override the App class.

_app.js
```
import React from 'react';
import App, { Container } from 'next/app';
import Navbar from "../components/Navbar";

export default class MyApp extends App {
  static async getInitialProps({ Component, router, ctx }) {
    let pageProps = {}

    if (Component.getInitialProps) {
      pageProps = await Component.getInitialProps(ctx)
    }

    return { pageProps }
  }

  render () {
    const { Component, pageProps } = this.props

    return (
      <Container>
      <Navbar />
        <Component {...pageProps} />
      </Container>
    )
  }
}
export default MyApp
```

- This is how _app.js can override the content on all our pages and we don't have to go to each page anymore and add the component, like navbar, footer, and manymore.

- 