---
layout: post
comments: true
title: "How To Add Custom Domain And SSL in Heroku"
---
<iframe width="560" height="315" src="https://www.youtube.com/embed/SqVvGx1XeUc" frameborder="0" allowfullscreen></iframe>

Although herkou provides its domain to all apps in form of `app-name.herokuapp.com`. We can also configure our own domain name in the app. This post is all about pointing custom domains to heroku app and also configuring SSL certificate.

**Note**: For setting up SSL on Heroku you need to upgrade to paid dyno in case you are using free one.
### Get Domain Name
We first need to purchase a domain name from domain providers such as Godaddy, Hostgator etc. You can also use free domains as well. For this post I am using a free domain name from [dotk](https://www.google.co.in/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwi4r_-t8_jUAhWIpo8KHV-wDEoQFghQMAE&url=http%3A%2F%2Fwww.dot.tk%2F&usg=AFQjCNGdnVqSIJXPBE3B0f-RHPo3W6fdYQ)
.

<!-- more -->

### Point Domain Name to Heroku App
Now we will make DNS changes to point domain to our app in heroku.
1. From heroku **dashboard** select the app which you want to configure for custom domain.
2. Now go to Domain Name and **Certificates section** in **Settings**. Click on **Add Domain** button and paste your domain name.<br>
You can also add domain via Heroku CLI.
 ```
 $ heroku add domains:add yourdomain
 ```
 and can also check the added domains.
 ```
 $ heroku domains
 ```

3. Update DNS of your domain name. Go to the DNS settings and add `CNAME` record with following values

 `Name`: yourdomainname

 `Value/Target`: yourdomainname.herokudns.com

 `TTL`: Leave it as it is

![DNS-Configuration]({{site.url}}/assets/dns-config.png)
**Note**: Replace yourdomainname with domain name you've purchased.

Visit https://yourdomainname and your app should be running on this domain now.

### SSL Configuration
You can purchase a SSL certificate from many providers in the market or can also generate ** Self Signed Certificate**. Although the process of adding SSL is same in both cases.

For this post I've used self signed certificate by following this guide [Heroku SSC Guide](https://devcenter.heroku.com/articles/ssl-certificate-self).

After getting the SSL certificate go to `Domain Name and Certificates` section in `Settings` in Heroku `Dashboard`.

![Heroku-SSL-Config]({{site.url}}/assets/ssl-config.png)

Go to `Configure SSL` -> `Manually`. Now paste certificate, key in the forms as asked and submit it. Now you've successfully configured the app with SSL.
