# PcmHammer.github.io

Repository for the PCM Hammer website

## Local Setup

You'll need .Net Framework 10

Visual Studio Code works fine. Proper Visual Studio doesn't add much, since 99% of the work here just in markdown files. I haven't needed to debug Statiq at all.

## Local Workflow

This uses Statiq to convert markdown and other files into an HTML website.

The development workflow:

1. Edit the files in the `input` directory tree
2. Run `dotnet run -- preview` to process the files
3. Generated files are written in the `output` directory tree, and a small HTTP server starts listening.
4. Point your browser at [http://localhost:5080/](http://localhost:5080/) to view the site.

Changes to files in the `input` tree are processed dynamically and will usually be visible in the browser within a few seconds.

We use the CleanBlog theme, which is fetched as a git submodule in the `theme` directory. In order to avoid having a separate repo for theme modifications, modified theme files are stored in the `theme-overlay` directory tree, and they are copied into `theme` as the first step of the build process. (This might create headaches if the theme repo changes in the future, but it hasn't been updated in 3 years.)

Note that changes to the overlay files are not processed in real time - you will need to exit and re-run the project to re-apply changes.

Also note that there is only one change in the overlay file, which changes the site title from "My Blog" to "PCM Hammer".

## Helpful Commands

* `dotnet run -- preview` - this will build the site and start an HTTP server on port 5080. Note that this command will never exis, because it continues to serve the site.
* `dotnet run` this will build the site and then exit.

## Deployment

Every merge to the Statiq branch triggers this GitHub workflow, which builds the HTML files uploads them to GitHub Pages automagically:

https://github.com/PcmHammer/PcmHammer.github.io/blob/Statiq/.github/workflows/publish-statiq.yml

# Resources

* Icons are from the [this collection](https://icons-for-free.com/themeisle_icons_graphics-icons-set/), which uses the Apache 2.0 license (very permissive)