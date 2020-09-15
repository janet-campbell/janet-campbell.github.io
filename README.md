<div align="center">
  <h1>

  ✍️

  Handmade Blog

  [![build](https://img.shields.io/github/workflow/status/ParkSB/handmade-blog/Node%20CI/master?style=flat-square)](https://github.com/ParkSB/handmade-blog/actions?query=workflow%3A%22Node+CI%22) ![node](https://img.shields.io/badge/node-%3E%3D%2010.0-brightgreen?style=flat-square) [![demo](https://img.shields.io/netlify/3f01acb3-1107-470a-914f-90d100b87d85?label=demo&style=flat-square)](https://handmade-blog.netlify.com/) [![license](https://img.shields.io/github/license/ParkSB/handmade-blog?style=flat-square)](LICENSE)

  </h1>
</div>

Handmade Blog is a classic static blog generator for people who want to start a blog quickly. It supports article type document for a blog post, work type document for portfolio, code highlights, [KaTeX](https://katex.org/) syntax, footnotes, and others.

## Demo: [Here](https://handmade-blog.netlify.com/)

![Article page preview](https://user-images.githubusercontent.com/6410412/74097056-be43d100-4b4a-11ea-806b-7bd263d7f623.png)

## Getting Started

1. Click the 'Use this template' button above the file list to create a new repository. If you want to use github.io domain, have to name the repository `{YOUR_ID}.github.io`.

2. Clone this repository, and install node modules.

    ```bash
    $ git clone https://github.com/{YOUR_ID}/{REPOSITORY_NAME}.git
    $ cd {REPOSITORY_NAME}
    $ npm install
    ```

3. Please create `development` branch and follow [this document](https://help.github.com/en/github/administering-a-repository/setting-the-default-branch) to set the branch to a default. Because GitHub pages hosts the site based on `master` branch. In addition, separating `master` branch and `development` branch is a good practice!

4. Modify `config.json` file in `services` directory to set your blog title and subtitle.

    ```json
    {
      "blogTitle": "Lorem Ipsum",
      "blogSubtitle": "lorem ipsum",
      "article": {
        "tableOfContents": true 
      }
    }
    ```

5. Start local server at `http://localhost:1234/`. `npm start` script opens local server based on `server` directory. It occurs an error because there aren't published articles and works pages yet.

    ```bash
    $ npm start
    ```

6. Publish the example articles and works by `npm run publish`. It converts a markdown documents in `_articles` or `_works` directory to HTML files.

    ```bash
    $ npm run publish article
    $ npm run publish work
    ```

7. Run `deploy` script if you're ready to host a live server. This script builds local files to `dist` directory and pushes it to `master` branch that contains only the files in `dist` directory. GitHub will host live server at `https://{YOUR_ID}.github.io/` based on `master` automatically.

    ```bash
    $ npm run deploy
    ```

## Usage

### Writing and publishing document

1. Write a document in `_articles` or `_works` directory.

1. Run `npm run publish article` or `npm run publish work` script to convert markdown to HTML.

1. Preview converted document on the local server using `npm start` script.

1. Run `npm run deploy` to publish the document to live server.

### Changing content of the page

Modify an ejs template to change the contents of the existing page. For example, if you want to put an image to the landing page, open the `app/templates/index.ejs` file, and add `img` tag to the `main-container` element.

```html
<main id="main-container">
  <img src="../assets/profile.jpg" alt="My profile picture" />
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</main>
```

Then, run `npm run publish page` script to publish the modified landing page.

```bash
$ npm run publish page
```

Done! You can change not only the landing page but any pages like this way. (You may need to understand the project structure.)

### Proejct structure

* `_articles` - Markdown files for the blog posts.
* `_works` - Markdown files for the portfolio.
* `app`
  * `assets` - Any files to be imported by HTML files such as image, font, etc.
  * `public` - HTML files generated by `publish` script. `server` and `dist` directory is based on this directory. Do not change the files under this directory directly.
    * `article` - HTML files converted from `_articles` directory.
    * `work` - HTML files converted from `_works` directory.
  * `src` - Source code to be imported by HTML files.
    * `css` - CSS files generated by `build` script.
    * `scss`
    * `ts`
  * `static` - Any static files that aren't compiled by `build` script like `robots.txt`, `sitemap.xml`, or SEO files. `build` script copies all files under this directory to `dist` directory. 
  * `templates` - HTML files used as ejs template. `publish` script converts a markdown file to HTML based on templates under this directory.
* `dist` - Files compiled by `build` script. `deploy` script deploys a website to GitHub pages based on this directory. Do not change the files under this directory directly.
* `server` - Files compiled by `build` script. `start` script opens local server based on this directory. Do not change the files under this directory directly.
* `services` - Source code implementing `publish` script.
  * `classes`
  * `models`
* `tools` - Source code implementing various npm scripts.

## Showcase

* parksb.github.io: https://github.com/parksb/parksb.github.io

## Available Scripts

### `npm start`

Starts local development server at http://localhost:1234/.

### `npm run publish`

Converts templates to HTML files.

```bash
$ npm run publish article
```

Converts all articles.

```bash
$ npm run publish works
```

Converts all works.

```bash
$ npm run publish article 5
```

Converts an article which id is 5.

```bash
$ npm run publish work 3
```

Converts a work which id is 3.

```bash
$ npm run publish page
```

Converts all pages.

### `npm run watch`

Rebuilds template files in `templates` directory and markdown files in `_articles` directory automatically whenever the files are modified.

### `npm run build`

Builds files with parcel bundler.

### `npm run deploy`

Builds and deploys the files.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
