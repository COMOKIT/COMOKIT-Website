<p align="center">
  
  <p align="center">
    COMOKIT-Website 📘
    <br />
    <br />
    <a href="https://github.com/COMOKIT/COMOKIT-Website/blob/master/LICENSE"><img src="https://img.shields.io/github/license/COMOKIT/COMOKIT-Website" alt="License" /></a>
    ·
    <a href="https://github.com/COMOKIT/COMOKIT-Website/issues"><img src="https://img.shields.io/github/issues/COMOKIT/COMOKIT-Website" alt="GitHub issues" /></a>
    ·
    <a href="https://github.com/COMOKIT/COMOKIT-Website/graphs/contributors"><img src="https://img.shields.io/github/contributors/COMOKIT/COMOKIT-Website" alt="GitHub contributors" /></a>
    <br />
    <a href="https://github.com/COMOKIT/COMOKIT-Website/actions"><img src="https://github.com/COMOKIT/COMOKIT-Website/workflows/Jekyll%20site%20CI/badge.svg?branch=master" alt="Jekyll site CI" /></a>
    ·
    <a href="https://github.com/COMOKIT/COMOKIT-Model/releases/latest"><img src="https://img.shields.io/github/v/release/COMOKIT/COMOKIT-Model?label=COMOKIT%20release" alt="COMOKIT Release version" /></a>
  </p>
</p>

This repository holds the Jekyll sources of the COMOKIT website!

## How the website works

There's 3 important place :
- `/` The landing page of the website (isn't not generated yet => Raw HTML page)
- `/docs` The generated documentation (use Jekyll x [Just-The-Doc](https://github.com/pmarsceill/just-the-docs))
- `/ressources` Recommanded place to upload big/extra files (ODD PDF, etc)

### I want to update the documentation

Please go to the `/docs/docs/` sub-folder to edit/add page (written in MarkDown) ;)

[> Click me <](https://github.com/COMOKIT/COMOKIT-Website/tree/master/docs/docs)

The documentation part is using the [Just-The-Doc](https://github.com/pmarsceill/just-the-docs) framework. If you have some interrogation on how to edit the page, please refere to the [official documentation](https://pmarsceill.github.io/just-the-docs/)

## Technical part (Documentation part)

### Local installation & Setup

First of all, make sure ruby is intalled on your computer.

1. Clone the repo `git clone https://github.com/COMOKIT/COMOKIT-Website.git`
1. Move in the folder `cd COMOKIT-Website/docs`
1. Install the JTD framework `gem install just-the-docs`
1. (Optional) Enable search `bundle exec just-the-docs rake search:init`
1. Install plugins: `bundle install --full-index`
1. Build your site: `bundle exec jekyll serve`
1. Connect to your running instance [http://127.0.0.1:4000/docs/](http://127.0.0.1:4000/docs/)

### Global configuration of the doc part

All the global configuration of the site can be found in the file [`_config.yml`](https://github.com/COMOKIT/COMOKIT-Website/blob/master/_config.yml) which is structured as follow :

## Bugs and Issues

Have a bug or an issue with this template? [Open a new issue](https://github.com/COMOKIT/COMOKIT-Website/issues/new) here on GitHub!

## Made with

* Pipeline
  * Jekyll
  * GitHub Actions
  * GitHub Pages

* Front-end
  * Raw HTML - Landing Page
  * [Just-The-Doc](https://github.com/pmarsceill/just-the-docs) - Jekyll framework

## Copyright and License

The COMOKIT project is licensed under the [***GPL-3.0 License***](https://github.com/COMOKIT/COMOKIT-Model/blob/master/LICENSE).
