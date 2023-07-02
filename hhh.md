#I came across this post Setting up SSL on Github Pages and wanted to try it out, but since my website set-up is a bit different than Keanu’s I had to go through a slightly different route. One reason being that this website is hosted on the apex (root) domain i.e. without www. This guide is focused towards an Octopress blog with a Custom Domain hosted through Github Pages, but this should work for Jekyll Static Sites as well.
#Getting Started
#(Almost the same as Keanu’s points)
#Sign up for Cloudflare if you don’t already have an account
#Add your website, and make sure all automatically generated records match those on your registrar’s website
#If you already have a gh-pages website and are simply moving to https, you don’t need to do anything else
#If not, and are trying to set up your site at apex, create an A record pointing to Github’s IP addresses, else a CNAME pointing to your-username.github.io
#Make sure there’s a CNAME file at the root of your gh-pages repo with your domain name
#Go to your Domain Registrar’s website and change the Domain Name Servers to those Cloudflare provides you with
#Finish Setting up your Domain on Cloudflare and go to the Domain Dashboard
#Open the “Cloudflare Settings” for your domain, and change the SSL Setting to “Flexible SSL”
#After a couple of hours, you’ll be able to open yoursite.com with https. But now comes the important part, letting search engines know and making your users use the SSL version.
#Letting Search Engines know
#In your _config.yml, add these:

#1
#2
#3
#4
#5
#6

url: https://www.yoursite.com   # with the https protocol
enforce_ssl: www.yoursite.com   # without any protocol

# For example, my configuration is this:
#url: https://sheharyar.me
#enforce_ssl: sheharyar.me

#Make sure you have a canonical link in your <head>:

#1

<link rel="canonical" href=" { { site.url } }{ { page.url } }" />

#If you’re on Octopress, then you probably already have the cooler version that creates beautiful canonical links.
#Redirect users to https
#Add this script to the very top of your <head>:

#1
#2
#3
#4
#5

<script type="text/javascript">
    var host = "yoursite.com";
    if ((host == window.location.host) && (window.location.protocol != "https:"))
        window.location.protocol = "https";
</script>


#Issues?
#If you find some stylesheets/scripts missing, make sure that you’re using the new https paths for your resources. A better option would be to not use the protocol at all:
#1
#2
#3
#4
#5

<!-- Change this -->
<link rel="stylesheet" href="http://www.somesite.com/path/to/styles.css">

<!-- to this: -->
<link rel="stylesheet" href="//www.somesite.com/path/to/styles.css">