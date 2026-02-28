# PcmHammer.github.io

Repository for the PCM Hammer website

## Local Workflow

This uses Statiq to convert markdown and other files into an HTML website.

The development workflow looks like this:

1. Edit the files in the `input` directory tree
2. Run `dotnet run -- preview` to process the files
3. Generated files are written in the `output` directory tree
4. Point your browser at [http://localhost:5080/](http://localhost:5080/) to view the site.
5. Changes to files in the `input` tree are processed dynamically and will usually be visible in the browser within a few seconds.

We use the CleanBlog theme, which is fetched as a git submodule in the `theme` directory. In order to avoid having a separate repo for theme modifications, modified theme files are stored in the `theme-overlay` directory tree, and they are copied into `theme` as the first step of the build process. (This might create headaches if the theme repo changes in the future, but it hasn't been updated in 3 years.)

Note that changes to the overlay files are not processed in real time - you will need to exit and re-run the project to re-apply changes.

Also note that there is only one change in the overlay file, which changes the site title from "My Blog" to "PCM Hammer".

# Helpful Commands

* `dotnet run -- preview` - this will build the site and start an HTTP server on port 5080. Note that this command will never exis, because it continues to serve the site.
* `dotnet run` this will build the site and then exit.

# Resources

* Icons are from the [this collection](https://icons-for-free.com/themeisle_icons_graphics-icons-set/), which uses the Apache 2.0 license (very permissive)