# Astro Fakestore

We would like to apologize if you were kept awake by the fact that we created a Fake Store site (recap exercise) which heavily depended on client-side javascript.

Since then, we've learned a lot of new things in the course, and we would like to make it up to you by creating a new version of the Fake Store site, but this time with Astro!

## Astro setup

- Create a new -Empty- Astro project to get started. Initialize a git repository and make your first commit.
- Create a repo on GitHub and push your local repo to GitHub.
- Create a new feature branch called `feature/layout` and switch to that branch.
- Create a base layout, move everything from the `index.astro` to there since we will be using it on all pages. Use the BaseLayout in the `index.astro` page.
- Add the Google font data to the base layout, so it's available on all pages.

  ```html
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Roboto+Slab:wght@400;800&display=swap"
    rel="stylesheet"
  />
  ```

- Set the `<slot/>` tag in a `<main>` tag in the body of the base layout.
- Make sure we can add something to the title of the page (hint: props)
- Commit your changes, push to GitHub, open a PR and merge it with the main branch.
  Locally, switch back to the main branch and pull the changes.

### CSS

We will use some site-wide CSS, the rest will be component specific.

- Create a new feature branch called `feature/style` and switch to that branch.

- In a `styles` directory, add a `reset.css` file
- Add a `global.css` file to the `styles` directory with the following content:

  ```css
  html {
    box-sizing: border-box;
  }
  *, *::before, *::after {
    box-sizing: inherit;
  }

  img {
    max-width:  100%;
    height: auto;
  }

  .visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
  }

  :root {
    --s_2: .2rem;
    --s_1: .5rem;
    --s1: 1rem;
    --s2: 1.2rem;
    --s3: 1.5rem;
    --s4: 2rem;

    --fs-s: .8rem;
    --fs-m: 1rem;
    --fs-l: 1.5rem;
    --fs-xl: 2rem;

    --c-bg1: #8EC5FC;
    --c-bg2: #E0C3FC;

    --c-dark: #4c4c4c;
    --c-mid: #757575;
    --c-primary: #ff3f40;

    --border-radius: .25rem;
    --border-radius-xl: 1rem;

    --maxContent: 60rem;
    --defaultShadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
  }


  body {
    line-height: 1.5;
    color:var(--c-dark);
    padding: clamp(1rem, 5vw, 5rem);

    background-color: var(--c-bg1);
    background-image: linear-gradient(80deg, var(--c-bg1) 0%, var(--c-bg2) 100%);

    font-family: 'Roboto Slab', serif;
  }
  ```

- Commit your changes, push to GitHub, open a PR and merge it with the main branch.
  Locally, switch back to the main branch and pull the changes.

## Header component

- Create a new feature branch called `feature/header` and switch to that branch.

- Create a new component called `Header.astro` and add it to the base layout.
- Add the following HTML to the component:

  ```html
  <header>
    <h1><a href="/">Fake Astro Store</a></h1>
  </header>
  ```

- This is the CSS for that component

  ```css
    h1 {
    background-color: white;
    color: var(--c-primary);
    padding: var(--s1) var(--s3);
    font-size: clamp(2rem, 5vw, 4rem);
    font-weight: 800;
    border-radius: var(--border-radius-xl);
    line-height: 1;

    text-align: center;
    display: block;
    margin-bottom: var(--s4);
  }

  a {
    text-decoration: none;
    color: inherit;
  }

  a:hover {
    color: var(--c-dark);
  }
  ```

- Commit your changes, push to GitHub, open a PR and merge it with the main branch.
  Locally, switch back to the main branch and pull the changes.

## Products collection

- Create a new feature branch called `feature/products` and switch to that branch.

We will make a [content collection](https://docs.astro.build/en/guides/content-collections/#what-are-content-collections) for the products. This is a great way to work with data in Astro, perfect for data that doesn't change often. We will assume that the products in our Fake Store don't change that often. Start by downloading the results of <https://fakestoreapi.com/products> and save it as a `products.json` file in the `src/data` directory.

### Define the collection

Create a new file `src/content.config.js` and setup the products collection. Since we have a JSON file, we will make use of the file loader. Check [this example](https://docs.astro.build/en/guides/content-collections/#built-in-loaders) to get started.

To make our application less error-prone, we will define a [schema](https://docs.astro.build/en/guides/content-collections/#defining-the-collection-schema) for our products using [Zod](https://docs.astro.build/en/guides/content-collections/#defining-datatypes-with-zod).

Analyze and implement the following schema, it's not that hard:

```js
schema: z.object({
  id: z.number(),
  title: z.string(),
  price: z.number(),
  description: z.string(),
  category: z.string(),
  image: z.string(),
  rating: z.object({
    rate: z.number(),
    count: z.number(),
  }),
}),
```

### Using the collection

To use the items in our collection, we can use Astro's [getCollection](https://docs.astro.build/en/guides/content-collections/#querying-collections).

Be aware that the items you get back are [wrapped in an object](https://docs.astro.build/en/guides/content-collections/#using-content-in-astro-templates) with a `data` property. So to access the title of a product, you need to use `product.data.title`.

Next step is to effectively use the products in our application:

## Products

- Create a new component called `ProductsList.astro` and add it to the index.astro page.
- In the [component script](https://docs.astro.build/en/core-concepts/astro-components/#the-component-script) get the products from the collection using `getCollection`.
- In the [component template](https://docs.astro.build/en/core-concepts/astro-components/#the-component-template) loop over the products and show them in a list. For now, just the title of the product is enough.

- Commit your changes, push to GitHub, open a PR and merge it with the main branch.
  Locally, switch back to the main branch and pull the changes.

## Product card

- Create a new feature branch called `feature/product-card` and switch to that branch.

We could create a product card directly in the products list, but we will create a separate component for it. Reusability ftw!

- Create a new component called `ProductCard.astro`
- Destructure the 'product' variable from the props in the component script.
- Add the HTML to show the product, something like this: (implement the product details with the data from the product variable)

  ```html
   <article>
    <img src="Product image url"
      alt="Product image"
      width="300"
      height="400"
    />
    <h3>Product title</h3>
    <p class="description">
      Product description
    </p>
    <p class="price">&euro; <span>Product price</span></p>
    <button>Buy now</button>
  </article>
  ```

- Style it with some CSS

```css
 article {
    height: 100%;

    background-color: white;
    border-radius: var(--border-radius);
    box-shadow: var(--defaultShadow);
    position: relative;

    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto min-content;
    grid-template-areas:
      "img img"
      "title title"
      "desc desc"
      "price cta";

    align-items: flex-start;
    gap: var(--s1);

    padding: var(--s2);

    max-width: var(--maxContent);
    margin: 0 auto;
    margin-bottom: var(--s3);
  }

  article:hover {
    box-shadow: rgba(0, 0, 0, 0.4) 0px 4px 12px;
  }

  h3 {
    font-size: var(--fs-l);
    font-weight: 900;
    grid-area: title;
  }

  img {
    aspect-ratio: 3/4;
    object-fit: contain;

    grid-area: img;

    justify-self: center;

    padding: var(--s1);
  }

  .description {
    grid-area: desc;
    align-self: baseline;

    display: -webkit-box;
    -webkit-line-clamp: 4;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;

    color: var(--c-mid);
  }

  .price {
    color: var(--c-primary);
    grid-area: price;
    line-height: 1;
    align-self: flex-end;
  }

  .price span {
    font-size: var(--fs-l);
  }

  button {
    grid-area: cta;
    align-self: flex-end;

    background-color: var(--c-primary);
    color: white;
    border: none;
    padding: var(--s_2) var(--s_1);
    font: inherit;
    outline-color: var(--c-primary);
    outline-offset: var(--s_2);
  }

  button:hover {
    background-color: var(--c-dark);
  }
  ```

- Use this `ProductCard` in the ProductsList component to show the products. It can be something like this: (note the use of `product.data`)

  ```jsx
  <ul>
  {
    products.map((product) => (
      <li>
          <ProductCard product={product.data} />
      </li>
    ))
  }
  </ul>
  ```

- We just have to add some CSS to style the product list. Here you have it:

  ```css
  ul {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
    grid-gap: var(--s4);
  }

  a {
    text-decoration: none;
    color: inherit;
  }
  ```

- We don't show if a product is popular or not. Let's fix this. First add the CSS:

  ```css
  .popular::after {
    content: "";
    background-color: var(--c-primary);
    position: absolute;
    top: 0;
    right: 0;
    width: 4em;
    height: 4em;
    padding-top: 2em;
    clip-path: polygon(0 0, 100% 0, 100% 100%);
  }

  .popular::before {
    content: "Top rated";
    color: white;
    position: absolute;
    top: 1.4em;
    right: 0;
    rotate: 45deg;
    z-index: 2;
    font-size: 0.7em;
  }
  ```

Now, add a conditional rendering to the class attribute of the article tag in the `ProductCard` component. Only add the class `popular` to the article tag when the `rating.rate` property is higher than 4.5

Et voilà, our index page is done!

- Commit your changes, push to GitHub, open a PR and merge it with the main branch.
  Locally, switch back to the main branch and pull the changes.

## Product detail page

- Create a new feature branch called `feature/product-detail` and switch to that branch.

We will create a detail page for a product. A user will be able to click on a product card on the homepage and get a detail page for that specific product. We will use the same ProductCard component but style it differently using container queries.

- In the `pages` directory, create a new directory `products` with an `[id].astro` file in it.
- We will be using dynamic routes to create all the product pages at build time. See [Dynamix routes (SSG mode)](https://docs.astro.build/en/core-concepts/routing/#static-ssg-mode) for more info. Inside the `getStaticPaths` function, get all products from the collection and return an array of objects with the product ID's. Something like this:

  ```js
  return products.map(product => ({
    params: { id: product.data.id.toString() },
    props: {
      product
    },
  }));
  ```

- Now, get the product data from the props, include the `ProductCard` component and pass the product data to it. Don't forget to add the BaseLayout to the page. Don't worry about the styling, we will fix that in the coming steps.
- Before we forget, wrap the `ProductCard` component in the `ProductsList` with an anchor tag to link to the detail page like this:

  ```jsx
  <a href={`/products/${product.data.id}`}>
    <ProductCard product={product.data} />
  </a>
  ```

- Commit your changes, push to GitHub, open a PR and merge it with the main branch.
  Locally, switch back to the main branch and pull the changes.

### Paging

- Create a new feature branch called `feature/paging` and switch to that branch.

We will let the user browse to a previous or next product via the detail page. For this to work, we need the previous and next product (if any) and a component that renders the paging links.

- Create a new component called `PrevNext.astro` and destructure the `prev`, `next` and `path` props in the component script. If we can set the `path` via props, we can use this component for other occasions as well.
- Noting really spectacular in here, so this is the CSS and HTML

  ```JSX
  <nav>
  <ul>
    {
      prev && (
        <li>
          <a href={`/${path}/${prev.id}`}>Previous</a>
        </li>
      )
    }
    {
      next && (
        <li class="right">
          <a href={`/${path}/${next.id}`}>Next</a>
        </li>
      )
    }
  </ul>
  </nav>
  ```

  ```CSS
  nav {
    background-color: white;
    border-radius: var(--border-radius-xl);
    margin-right: auto;
    margin-left: auto;
    padding: var(--s1) var(--s4);
    max-width: var(--maxContent);
  }

  ul {
    display: flex;
    justify-content: space-between;
  }

  .right {
    margin-left: auto;
  }
  ```

- To implement this on our detail page, we need to provide a previous and next property to the page props.

  ```js
  next: i < products.length - 1 ? products[i + 1] : null,
  prev: i > 0 ? products[i - 1] : null,
  ```

- Add the `PrevNext` component to the detail page and pass the `prev`, `next` and `path` props to it. The `path` will be `products` in this case.
- Check if you can navigate to the previous and next product. And back and forth to the index page.

- Commit your changes, push to GitHub, open a PR and merge it with the main branch.
  Locally, switch back to the main branch and pull the changes.
