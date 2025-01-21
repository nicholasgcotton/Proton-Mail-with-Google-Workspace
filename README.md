# Proton Mail with Google Workspace
How to set up split delivery so you can use two email servers with one domain, specifically for Google Workspace (Gmail) and Proton Mail.

In searching the Proton Mail support forums and online I could not find instructions on how to do this, and further found a couple folks claiming that it was impossible. 

## Overview

Using Google Workspace as the advertised MX server, you can re-route specific accounts to Proton Mail and send/recieve from that account on Proton Mail, without creating any copies of the email in the Google Workspace account. Google Workspace has a setting to run "default routing" rules on incoming emails before they are fully processed by the mailserver. The email metadata will be logged, but as far as I can tell Google will not retain a copy of the messag at all (if the below instructions are followed).

### Setup Overview
1) Domain.com MX server is set to Google ([follow Google Workspace instructions to add a domain](https://support.google.com/a/answer/7502379?product_name=UnuFlow&hl=en&visit_id=638730817709681273-622307060&rd=1&src=supportwidget0&hl=en), or start from having a working domain at Workspace already set up and working with Gmail).
2) Start the procees of [adding as domain to Proton Mail](https://proton.me/support/custom-domain), and create the user@domain.com acccount within Proton mail. You must add the account within Proton Mail before re-directing email from Google workspace or it will not be accepted.
3) Note the MX server settings for Proton Mail (currently mail.protonmail.ch:25).
4) In Google Workspace admin add the Proton Mail MX server under "Hosts".
5) In Google Workspace admin add the route to Proton mail for the desired user@domain.com under the "default routing" rules, using the MX server set in the previous step.
6) If you want to set a catch-all email to the user@domain.com account that you have moved to Proton Mail, you must set it within Google Workspace and NOT within Proton Mail, or else messages sent from Proton Mail to other @domain.com email address will not leave the Proton Mail server, and will just loop back to user@domain.com.


## Detailed Instructions

### Part 1: Setup Proton Mail Settings and Domain.com DNS Records

- Following all Proton Mail setup instructions for the DNS on domain.com EXCEPT for DMARC (will show unset) (still testing) and MX server (will show error state). Catch-all should not be set within Proton Mail, it can only be congfigured in Google Workspace settings under this setup, otherwise any email from the Proton user@doimain.com account will not be delivered to the Google MX servers. 

- Instructions: [How to use a custom domain with Proton Mail](https://proton.me/support/custom-domain)

- Results should look like this:
![image showing proton mail configuration with all items except DMARC (unset) and MX server (error status) configured green](https://github.com/nicholasgcotton/Proton-Mail-with-Google-Workspace/blob/main/screenshots/Proton%20Mail%20Domain%20Settings.png)


### Part 2: Setup Google Workspace Gmail Settings

The following items are found at [Google Workspace Admin](https://admin.google.com) under Apps, Google Workspace Apps, Gmail.

- Under "Hosts" add the Proton Mail MX server as an alternative server for the domain.
![Google hosts settings showing proton mail mx server: mail.protonmail.ch, port 25, require TLS yes, require certificate yes](https://github.com/nicholasgcotton/Proton-Mail-with-Google-Workspace/blob/main/screenshots/Google%20Hosts%20Settings%20for%20Proton%20Mail.png)

- Under "Default Routing" create a new rule for the email address in qustion, and set it so that the options for "Route" are set to "change route", with "also reroute spam" and select the alternative MX server that was created in the previous setup step. Also select "bypass spam filter for this message", and "perform this action on recognized and non-recognized addresses". ![Google Workspace "Default Routing" setup as described in the previous paragraph](https://github.com/nicholasgcotton/Proton-Mail-with-Google-Workspace/blob/main/screenshots/Google%20User%20Routing%20Part%201.png)
![Google Workspace "Default Routing" setup as described in the previous paragraph](https://github.com/nicholasgcotton/Proton-Mail-with-Google-Workspace/blob/main/screenshots/Google%20User%20Routing%20Part%202.png)
![Google Workspace "Default Routing" setup as described in the previous paragraph](https://github.com/nicholasgcotton/Proton-Mail-with-Google-Workspace/blob/main/screenshots/Google%20User%20Routing%20Part%203.png)

#### Optional Setup for Catch All address
- Under "Email Routing" set a catch all address for the domain. If you are using a catch all address it must be set in Google Workspace and not in Proton Mail.
- ![Google Email routing settings showing "user@domain.com" as the catch all address for the domain](https://github.com/nicholasgcotton/Proton-Mail-with-Google-Workspace/blob/main/screenshots/Google%20Email%20Routing%20Catch%20All.png)
