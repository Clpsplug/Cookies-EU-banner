# Cookies EU banner

Manage display of banner to accept/reject cookies from tracking services like Google Analytics.


## Installation

### Get the script

Use bower : `bower install cookies-eu-banner --save`  
Or [download the latest version](https://github.com/Alex-D/cookies-eu-banner/archive/master.zip).


### In your pages

Insert the banner before any content at the beginning of the `<body>` element, with these IDs:

```html
<div id="cookies-eu-banner" style="display: none;">
    En poursuivant votre navigation sur ce site, vous acceptez l'utilisation de cookies par Google Analytics pour réaliser des statistiques de visites.
    <a href="./en-savoir-plus.html" id="cookies-eu-more">En savoir plus</a>
    <button id="cookies-eu-reject">Je refuse</button>
    <button id="cookies-eu-accept">J'accepte</button>
</div>
```


- `#cookies-eu-banner` is the div that contains all elements to be hidden after user accepts or declines the use of cookies;
- `#cookies-eu-more` is a link to a "Read more" page where you explain your use of cookies;
- `#cookies-eu-reject` and `#cookies-eu-accept` are the buttons used to reject/accept cookies.


Before the end of `<body>`, or in a script file inserted at the same place, put the following code:

```html
<script src="./cookies-eu-banner.min.js"></script>
<script>
    new CookiesEuBanner(function(){
        // Your code to launch when user accept cookies
    });
</script>
```

Example for Google Analytics:

```html
<script src="./cookies-eu-banner.min.js"></script>
<script>
    new CookiesEuBanner(function(){
        (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
        (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
        m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
        })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

        // Don't forget to put your own UA-XXXXXXXX-X code
        ga('create', 'UA-XXXXXXXX-X', 'auto');
        ga('send', 'pageview');
    });
</script>
```


## How does it works?

For a detailed explaination, see comments in the main file : [cookies-eu-banner.js](cookies-eu-banner.js).

In short:

1. Excludes bots, clients who have DoNotTrack activated, and users who have already declined;
2. Runs your custom function if user has already accepted;
3. Shows banner, then:
    - if user accepts, run custom function and put a cookie to save this acceptance;
    - if user declines, remove all Google Analytics cookies and put a cookie to save this rejection.


## Functionalities

- Do Not Track detection (IE9+, Firefox, and all browsers compatible with the `navigator.doNotTrack` JavaScript variable);
- Disables banner when visitor is a bot : prevents SEO Engines to confuse your cookie advert message with the main content of your pages;
- Respects [all points imposed by CNIL (FR)](http://www.cnil.fr/vos-obligations/sites-web-cookies-et-autres-traceurs/outils-et-codes-sources/la-mesure-daudience/) and [these points](http://www.cnil.fr/vos-obligations/sites-web-cookies-et-autres-traceurs/que-dit-la-loi/).


## Supported browsers

All navigators which supports JavaScript. Take a look at [navigators that implements DoNotTrack](http://donottrack.us/).
