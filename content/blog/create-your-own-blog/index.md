---
title: How I created this blog using Gatsby and Netlify
date: "2020-03-15T22:40:32.169Z"
description: Learn how to create your own blog using static-site generator like Gatsby and deploy it with the help of Netlify.
---

Starting a blog could be sometimes difficult. You have to come up with a name, set it up somehow, figure out where to host it… it’s enough to make you just give up and go write on Medium (or not at all) and pay unnecessary commission for your content. 

Even, If you manage to get started, there are yet more obstacles. How can you grow an audience if you’re starting from zero? How do you figure out what to write about? And then – how do you keep writing, even when you don’t feel like it? In all this cumbersome process one can lose a lot of time in setting up the blog.

So that’s why I have written this article. It starts with zero assumptions about your level of understanding Gatsby and walks through every step of the process. And Don't worry, I will walk you through everything you need to know. In this article we will cover:

    1. How to set up a blog in under 15 minutes with GatsbyJS
    2. How to host it for free on Netlify

### 🚀 Let's Go

Let's talk about [Gatsby](https://www.gatsbyjs.org/). It’s a static site generator written in JavaScript and backed by React and GraphQL, and it’s gaining a ton of popularity lately.

I’m brand new to Gatsby myself, and I thought I’d want share this guide as this blog was itself created using gatsby.

Gatsby allows you to write in [Markdown](https://en.wikipedia.org/wiki/Markdown), a simple plain text format that’s easy to learn and easy to write with. Gatsby then takes the Markdown files and generates the HTML blog posts. Also this doesn't mean that Gatsby is only for blogs but you can create a lot more like a e-commerce website – but since we’re talking about blogs here, I’ll keep things focused on the blogging use case.

Let’s walk through setting up your blog right now. You’ll need to make sure Node and NPM installed. If not, check how to install [Node and NPM](https://nodejs.org/) first.

  1.  **Create a Gatsby site.**

      First, install the Gatsby CLI. This will give you the 'gatsby' command:

      ```shell
        npm install -g gatsby-cli
      ```
      Use the Gatsby CLI to create a new site, specifying the blog starter.

      ```shell
        gatsby new <my-new-blog-directory> https://github.com/gatsbyjs/gatsby-starter-blog
      ``` 
      Now, Navigate into your new site’s directory and start it up.

      ```shell
        cd <my-new-blog-directory>
        gatsby develop
      ```

  2.  **Open the source code and Make It YOUR OWN!**

      Your site is now running at `http://localhost:8000`!
      Note: You'll also see a second link: _`http://localhost:8000/___graphql`_. This is a tool you  can use to experiment with querying your data. Learn more about using this tool in the [Gatsby tutorial](https://www.gatsbyjs.org/tutorial/part-five/#introducing-graphiql).

      Open the `my-new-blog directory` in your code editor of choice and edit `src/pages/index.js`. Save your changes and the browser will update in real time!

      Open up the `gatsby-config.js` file in the root directory, and customize the `siteMetadata` stuff at the top. **Kyle Mathews is great but this is YOUR blog**, now.

      Scroll down a little further and read through the list of plugins, if you like. Or just ignore them for now.

      Update the image at `content/assets/profile-pic.jpg` to be **your own face** instead of Kyle’s.

      **Some Quick Tips:**

      - **`/src`**: This directory will contain all of the code related to what you will see on the front-end of your site (what you see in the browser) such as your site header or a page layout. `src` is a convention for “source code”. For-example, if you want to modify your bio say add another social account, then goto `/src/component/bio.js` and edit `href attribute` and link the username in `...\gatsby-config.js` 

      - **`gatsby-config.js`**: This is the main configuration file for a Gatsby site. This is where you can specify information about your site (metadata) like the site title and description, which Gatsby plugins you’d like to include, etc. (Check out the [config docs](https://www.gatsbyjs.org/docs/gatsby-config/) for more detail).

      - **If you are having a hard time figuring out what's going on inside the different files/directories, then dont't worry about it. Nobody is expecting you to figure-out everything on just first glance. Take your time!**

      If you want to know more about each directories in brief then visit this [link.](https://github.com/tarunv09/blog-demo/blob/master/README.md)


  3.  **Write a New Post**

      This starter project is set up to look for blog posts under the `content/blog` directory (because `gatsby-config.js` told it to).

      To create a new post, you just need to create a new file in there, with a `.md` or `.markdown` extension. To try it out, create a file called `first-post.md` under `content/blog`. Inside this file, write this out:

      ```shell
        ---
        title: My First Post
        ---

        Hello World, Welcome my new blog!
        The stuff at the top inside the dashes is called “frontmatter”. Here you can set the title, date, and other metadata about the post. The frontmatter won’t appear in the final document.
      ```

      As soon as you save this, the Gatsby development server will pick it up and re-generate the blog. If you have http://localhost:8000/ open already, it’ll hot-reload with your new post on the front page.

      Click on your new post. Oooh, it loads so fast! Ok, fine, it’s on localhost, and it has basically zero content, but still. It’s snappy. Gatsby makes fast sites.

      If you look at the URL bar, you’ll notice that Gatsby has used the filename as the URL, without the .md extension.

      Gatsby will also find files in subdirectories of content/blog, so you could create a new folder for each post if you want to. Look at the existing posts, and you’ll see that they exist as index.md files within directories. Further, notice how their URL is determined by the directory name.

      **Try This:**
      ```shell
        What happens if you create a similar file under the content/blog/hello-world directory?
        Does it appear on the front page? 
        What’s the resulting URL? 
        Does it all make sense? If not, edit as much as want!
      ```

  4. **Now It's Time to Push Your Blog to GitHub**

      Go to GitHub and create a new repo. **Don’t check “initialize the repo with a README”** because we’re going to import the everything pre-made from your machine.

      In your blog directory, initialize the Git repo, add the files, and commit them:

        git init
        git add .
        git commit -m "message"
        
      Then push the repo to GitHub:

        git remote add origin https://github.com/yourname/repo-name.git
        git push -u origin master
    
      If you refresh your blog’s GitHub repo now, you should see the README file that says **“Gatsby’s blog starter”**. With your blog up on GitHub, you can now deploy it to Netlify.

  5. **Finally, Deploy Your Gatsby Blog to Web using Netlify**

      
      Netlify is a great free hosting service for static sites. My own blog, the one you’re reading now, runs on Netlify. It’s easy to set up, and publishing new posts is as easy as git push.

      Create a new account at [Netlify](http://app.netlify.com/). Netlify can pull from GitHub, Bitbucket, and GitLab.

      Then sign in and click **“New Site from Git”**.

      Then choose Github, and authorize Netlify to access your Github account.

      Next you’ll **“install”** Netlify to your Github account. and set permissions according to your preference like limit its access to just the blog repo.

      Now you can choose the repository to deploy – pick the blog repo you created.

      On the next screen, click **“Deploy Site”**. After a minute or so of building, your site will be published and ready to view!

      It’ll have some sort of ugly URL by default, but Netlify makes it easy to point a custom domain at it if you have one. Netlify will set up free SSL for you, too. If you need a domain, you can try something like NameCheap (because I've been using them for free, thanks to [Github Student Developer Pack](https://education.github.com/pack)).

   ####By Now, you have:#####

        learn something new today 🎓  
        created a local dev environment 💻 where you can write posts and preview them
        deployed it over the web for free 🔥 
        ownership of your own content forever, Tada!🎉

   ####If you still get stuck, feel free to reach out to me on [Linkedin](https://in.linkedin.com/in/tarunv09) or visit [this blog's repo files on github](https://github.com/tarunv09/blog-demo). Also you can checkout the [official Gatsby youtube tutorial](https://www.youtube.com/watch?v=xJVHWhO9bJY) for better clarification. And if everything worked-out for you, then go ahead and Start Blogging!####