---
title: "Recipes: Transforming Data"
---

Transforming data in Gatsby is plugin-driven. Transformer plugins take data fetched using source plugins, and process it into something more usable (e.g. JSON into JavaScript objects, and more).

## Transforming Markdown into HTML

The `gatsby-transformer-remark` plugin can transform Markdown files to HTML.

### Prerequisites

- A Gatsby site with `gatsby-config.js` and an `index.js` page
- A Markdown file saved in your Gatsby site `src` directory
- A source plugin installed, such as `gatsby-source-filesystem`
- The `gatsby-transformer-remark` plugin installed

### Directions

1. Add the transformer plugin in your `gatsby-config.js`:

```js:title=gatsby-config.js
plugins: [
  // not shown: gatsby-source-filesystem for creating nodes to transform
  `gatsby-transformer-remark`
],
```

2. Add a GraphQL query to the `index.js` file of your Gatsby site to fetch `MarkdownRemark` nodes:

```jsx:title=src/pages/index.js
export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

3. Restart the development server and open GraphiQL at `http://localhost:8000/___graphql`. Explore the fields available on the `MarkdownRemark` node.

### Additional resources

- [Tutorial on transforming Markdown to HTML](/tutorial/part-six/#transformer-plugins) using `gatsby-transformer-remark`
- Browse available transformer plugins in the [Gatsby plugin library](/plugins/?=transformer)

# **Recipes: **Transforming an image with GraphQL

Transforming images into grayscale using GraphQL in Gatsby

## How Gatsby handles images using the Gatsby image API

gatsby-image is a React component designed to work seamlessly with Gatsby’s [native image processing](https://image-processing.gatsbyjs.org/) capabilities powered by GraphQL and [gatsby-plugin-sharp](https://www.gatsbyjs.org/packages/gatsby-plugin-sharp/) to easily and completely optimize image loading for your sites.

## Prerequisites

- A Gatsby site with `gatsby-config.js` and an `index.js` page
- The `gatsby-plugin-sharp` plugin installed
- an image (`.jpg`, `.png`, `.gif`, `.svg`, etc.) in the `src` folder

## Directions

1. To start working with Gatsby Image, install the `gatsby-image` package along with necessary plugins `gatsby-transformer-sharp` and `gatsby-plugin-sharp`. Reference the packages in your `gatsby-config.js` file. You can also provide additional options to <code>[gatsby-plugin-sharp](https://www.gatsbyjs.org/packages/gatsby-plugin-sharp/)</code> in your config file.

```JavaScript
npm install --save gatsby-image gatsby-plugin-sharp gatsby-transformer-sharp
```

```JavaScript
module.exports = {
 plugins: [
   `gatsby-transformer-sharp`,
   `gatsby-plugin-sharp`,
   {
     resolve: `gatsby-source-filesystem`,
     options: {
       path: `${__dirname}/src/data/`,
     },
   },
 ],
}
```

2. Set up a [GraphQL query](https://www.gatsbyjs.org/docs/graphql-reference/) and either pass it into a component as props or write it directly in the component. One technique is to leverage the <code>[useStaticQuery](https://www.gatsbyjs.org/docs/use-static-query/)</code> hook.

Common GraphQL queries for sourcing images include `file` from [gatsby-source-filesystem](https://www.gatsbyjs.org/packages/gatsby-source-filesystem/), and both `imageSharp` and `allImageSharp` from [gatsby-plugin-sharp](https://www.gatsbyjs.org/packages/gatsby-plugin-sharp/), but ultimately the options available to you will depend on your content sources.

3. Use the grayscale query option in `gatsby-plugin-sharp` settings in `gatsby-config.js,`this applies to both _fluid_ and _fixed_ images:

`grayscale` (bool, default: false)

```JavaScript
fixed(
 grayscale: true
)
```

4. Run `gatsby develop` to start the development server.

5. View your image in the browser: `http://localhost:8000/`

## Additional resources

- API docs, including grayscale and duotone query tips: [https://www.gatsbyjs.org/docs/gatsby-image/#shared-query-parameters](https://www.gatsbyjs.org/docs/gatsby-image/#shared-query-parameters)
- Gatsby Image docs: [https://www.gatsbyjs.org/packages/gatsby-image/](https://www.gatsbyjs.org/packages/gatsby-image/)
- Image processing examples: [https://github.com/gatsbyjs/gatsby/tree/master/examples/image-processing](https://github.com/gatsbyjs/gatsby/tree/master/examples/image-processing)

<!-- Docs to Markdown version 1.0β17 -->
