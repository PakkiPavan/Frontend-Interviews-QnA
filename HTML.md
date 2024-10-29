
Topics:
- Semantic elements
- New features in HTML5
- Meta tag in HTML
- Image Map in HTML
     - HTML image maps are used to create clickable areas on an image.
     - Image Map lets a developer map/link different parts of images with the different web pages.
     - It can be achieved by the ```<map>``` tag in HTML5, using which we can link images with clickable areas.
     - See this https://www.w3schools.com/html/html_images_imagemap.asp for reference.
```html
<img src=”image_url” usemap=”#workspace” />
<map name=”workspace”>
     <area shape=”rect” coords=”34, 44, 270, 350” href=”xyz.html” />
     <area shape=”rect” coords=”10, 120, 250, 360” href=”xyz.html” />
</map>
```

Void elements in HTML
- Void elements in HTML (also called self-closing or empty elements) are tags that do not require a closing tag. They cannot contain any content or child elements. 
- These elements are "self-contained" and are used for specific purposes, such as inserting images, line breaks, or metadata.

Example:
```html
<input />
<img src="image.jpg" alt="Description" />
```

```<!DOCTYPE>```
- The ```<!DOCTYPE>``` declaration in HTML is used to specify the version of HTML that the web page is written in.
- It helps web browsers interpret the document correctly by understanding the document type and rendering the page accordingly.
- This declaration tells the browser that the document is written in HTML5, the current standard for web pages.

meta tag:
- The ```<meta>``` tag in HTML is used to provide metadata about the web page, which is not directly displayed on the page but is essential for browsers, search engines, and other web services.
- Metadata can include things like the character set of the document, author information, keywords, page description, and how the page should be displayed or behave.

**Semantic elements:**  
Semantic elements are those which describe the particular meaning to the browser and the developer. Elements like ```<form>, <table>, <article>, <figure>``` etc., are semantic elements.

**New Features in HTML5:**
- New Semantic Elements − These are like ```<header>, <footer>, and <section>```.
- Forms 2.0 − Improvements to HTML web forms where new attributes have been introduced for ```<input>``` tag.
- Persistent Local Storage − To achieve without resorting to third-party plugins.
- WebSocket − A next-generation bidirectional communication technology for web applications.
- Server-Sent Events − HTML5 introduces events which flow from web server to the web browsers and they are called Server-Sent Events (SSE).
- Canvas − This supports a two-dimensional drawing surface that you can program with JavaScript.
- Audio & Video − You can embed audio or video on your webpages without resorting to third-party plugins.
- Geolocation − Now visitors can choose to share their physical location with your web application.
- Microdata − This lets you create your own vocabularies beyond HTML5 and extend your web pages with custom semantics.
- Drag and drop − Drag and drop the items from one location to another location on the same webpage.


1. Local Storage:
- Purpose: Stores data persistently in the browser. Ideal for saving data that doesn’t need to be sent to the server with each request.
- Storage Size: ~5 MB per domain (larger than cookies).
- Data Expiry: Data persists until explicitly deleted by the user or programmatically by the application.
- Accessibility: Accessible only on the client side (not sent to the server with every HTTP request).
- Use Cases: Storing user preferences, themes, or settings that need to persist across sessions but aren’t sensitive enough to require server-side storage.

2. Session Storage:
- Purpose: Stores data for the duration of the page session. Ideal for temporary data that only needs to exist while the page/tab is open.
- Storage Size: ~5 MB per domain (same as local storage).
- Data Expiry: Data is cleared when the tab or window is closed or the session ends (not persistent across sessions).
- Accessibility: Only accessible within the same tab/window and not shared between different tabs.
- Use Cases: Temporary storage of form data, one-time states, or data that’s only relevant to the current browsing session.


3. Cookies:
- Purpose: Primarily used for storing session data that needs to be sent to the server with every HTTP request (e.g., for authentication).
- Storage Size: ~4 KB per cookie (much smaller than Local/Session Storage).
- Data Expiry: Can be configured with an expiration date:
- Session Cookies: Deleted when the browser is closed (like session storage).
- Persistent Cookies: Expire after a set date, as specified by the Expires or Max-Age attribute.
- Accessibility: Sent to the server with every HTTP request, and can also be accessed on the client side via JavaScript (if the HttpOnly flag is not set).
- Use Cases: Storing user authentication tokens, session management, user preferences that need to be accessed by the server, etc.

Web Worker:
- A Web Worker in JavaScript is a feature that allows you to run scripts in the background, separate from the main thread of a web page. - This helps in performing tasks without blocking or slowing down the user interface (UI), improving the responsiveness and performance of web applications.

**Shadow DOM:**
- The Shadow DOM is a part of the Web Components specification in HTML that allows developers to encapsulate a portion of a DOM subtree.
- It helps in creating self-contained components with their own isolated DOM and CSS, ensuring that the component's structure and style do not interfere with or get affected by the rest of the document's DOM or styles.

**Key Features of Shadow DOM:**
- Encapsulation: The Shadow DOM isolates the internal structure and styles of a web component from the rest of the document. This means styles defined in the Shadow DOM don’t affect the rest of the page, and vice versa.

- Scoped Styles: CSS styles inside the Shadow DOM are scoped specifically to the elements within it. This prevents style leakage (global styles affecting components or component styles affecting global styles).

- Component Reusability: Shadow DOM is often used with Web Components (custom elements) to build reusable, modular components that maintain their internal behavior and appearance without conflicting with other components or styles on the page.

- DOM Isolation: Elements within the Shadow DOM are not accessible from the light DOM (the regular DOM structure of the page), providing an additional layer of protection and encapsulation for component logic.

**Why Use Shadow DOM?**
- Style Encapsulation: One of the main advantages of using Shadow DOM is that it solves the problem of global CSS conflicts. For example, if you have multiple components with the same class names or styles, Shadow DOM ensures that each component is styled independently.

- Component Isolation: It allows developers to create isolated components that can be reused across different projects or pages without worrying about affecting (or being affected by) external styles or scripts.

- Preventing Name Collisions: Shadow DOM ensures that IDs, classes, and styles used inside the component won’t conflict with those used elsewhere on the page.

- Web Components: Shadow DOM is a core technology for Web Components, which are a way to define custom HTML elements with their own encapsulated behavior and styles.

**When to Use Shadow DOM?**
- Building Reusable Components: If you're creating custom elements or reusable components (like a custom button or modal), Shadow DOM is a great way to encapsulate the component’s structure and styles.
- Avoiding Style Conflicts: For complex web applications where global CSS styles might interfere with individual components, Shadow DOM ensures components are immune to those conflicts.

**Responsive web design:**
- Responsive web design (RWD) is an approach to web development that ensures a website's layout and content adapt to various screen sizes and devices, such as desktops, tablets, and mobile phones.
- This approach improves usability and provides a better user experience across different devices.

1. Fluid Grids:
- Instead of using fixed-width layouts, a fluid grid system uses relative units like percentages or em to create a flexible layout.
- This allows elements to resize proportionally based on the screen size.

2. Flexible Images and Media:
- Images, videos, and other media should also be flexible.
- This is typically done using CSS to ensure that images resize within their containers.
- A common technique is to set the max-width of images to 100%, which makes them scale down as necessary but not stretch beyond their original size.

```css
img {
  max-width: 100%;
  height: auto;
}
```

3. Media Queries:
- Media queries allow designers to apply specific CSS rules based on device characteristics like screen width, height, orientation, and resolution.
- This is a key feature for adapting designs to different devices.

```css
@media (max-width: 768px) {
  /* Styles for tablets and smaller devices */
}

@media (min-width: 1024px) {
  /* Styles for desktops */
}
```

Shortcut to remember:  
max-width: 768px means <768px  
min-width: 768px means >786px

4. Viewport Meta Tag:
- This is crucial for ensuring that the layout adapts to mobile devices.
- The viewport meta tag tells the browser how to control the page's dimensions and scaling.
- Without it, mobile browsers tend to assume a fixed width, causing layout issues.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

5. Mobile-First Design:
- Start designing for the smallest screen sizes (usually mobile devices) first, and then progressively enhance the design for larger screens. This approach ensures that the design is optimized for the most constrained environments first.


Cross-Browser Compatibility:
- Cross-browser refers to the practice of designing and developing websites or web applications so that they work consistently across different web browsers.
- Since different browsers (such as Chrome, Firefox, Safari, Edge, etc.) may interpret HTML, CSS, and JavaScript slightly differently.
- Cross-browser compatibility ensures that users experience a consistent layout, functionality, and performance, regardless of which browser they use.
- Web browsers understand code slightly differently, so ensuring cross-browser compatibility is key to providing a consistent experience.

1. Vendor Prefixes for CSS:
- Different browsers may require vendor prefixes for newer CSS properties.

Example:
```css
.box {
  display: -webkit-flex; /* Safari */
  display: -ms-flexbox;  /* IE */
  display: flex;         /* Standard */
}
```

2. Testing in Different Browsers:
- Test your website in different browsers, including Chrome, Firefox, Safari, and Edge, as well as older versions of Internet Explorer if required.

3. Use of Polyfills:
- Polyfills allow older browsers to use modern JavaScript or CSS features.
- For example, using @babel/polyfill for JavaScript ES6 features or a CSS Grid polyfill for older browsers.


