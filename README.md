# RenderNow
A pre-render service for client-side rendered websites

# Prerendering
Prerendering involves using a headless browser on the server to load, execute JavaScript, and construct the DOM. This generated DOM is then converted into a string and sent back to the client.

![Dynamic Rendering Explainer](assets/Dynamic-Rendering-Explainer.png)

We determine if the request is from a crawler by inspecting the User-Agent header. [This is when we'll use this product as a middleware]
- **If the request is from a crawler**:
instruct Render-Now to prerender the current page and return the server-side rendered HTML.

- **If the request is not from a crawler**:
we simply return index.html, allowing the JavaScript files to handle client-side rendering.

### Features
- **🔍 Crawler Detection**: Inspects User-Agent headers to determine if a request is from a crawler. If so, it prerenders the page and returns server-side rendered HTML, enhancing SEO without impacting client-side performance.

- **🎯 Request Optimization**: Skips unnecessary requests, such as those for ads, trackers and CSS and Images files, during the prerendering process to improve performance and reduce tracking.

- **👩🏻‍💻  Self-healing**: RenderNow constantly checks the health of the browser instance and restart it if necessary.

- **💾 Caching for Performance**: Implements caching mechanisms to speed up subsequent responses, ensuring fast and efficient rendering.

- **🌐 Broad Compatibility**: Designed to work with a variety of APIs and services, making it adaptable to diverse environments and requirements.

# Route

#### `/render`
**Use Case:** Request an HTML rendered version of a webpage  
**HTTP Method:** GET or POST  

| Location   | Name                     | Default Value | Required | Comments                                                                                                                                   |
|------------|--------------------------|---------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------|
| QueryString | `url`                    | N/A           | Yes      | The URL to pre-render.                                                                                                                     |
| Body       | N/A                       | N/A           | No       |  skip the initial page load of the URL and use the content of the body to render the page. Should be of type `text/html`.      |
| HTTP Header | `block-ads`  | `false`       | No       | `true/false` to skip Ads/Trackers domains, improving performance and avoiding unnecessary tracking.           |

# Why Render-Now?
Prerendering is ideal in the following scenarios:

- **Enhancing SEO for an Existing SPA**: If you have an existing Single Page Application (SPA) and want to improve its SEO capabilities without overhauling the entire architecture, prerendering is a practical solution.

- **Non-Node.js Server-Side Applications**: If your server-side application is not built on Node.js, making traditional Server-Side Rendering (SSR) more challenging, prerendering offers a simpler alternative.

For new SPA projects where SEO is crucial, it's recommended to use Node.js and implement SSR with the appropriate framework from the start.

# Installation

set up environment variables - 

| Name          | Default Value |
|---------------|---------------|
| PORT          | `3000`        |
| CACHE_MAX_SIZE | `100 MB`        |
| CACHE_MAX_AGE | `1800 sec`        |


```sh
npm install
npm run dev
```
