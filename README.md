# Proton Mail with Google Workspace
How to set up split delivery so you can use two email servers with one domain. 

In searching the Proton Mail support and forums I could not find instructions on how to do this, and further found a couple folks claiming that it was impossible.

## Overview

Using Google Workspace as the advertised MX server, you can route specific accounts to Proton Mail and send/recieve from that account on Proton Mail, without creating any copies of the email in the Google Workspace account.
Google Workspace has a setting to run "default routing" rules on incoming emails before they are fully processed by the mailserver. The email metadata will be logged, but as far as I can tell Google will not retain a copy of the messag at all (if the below instructions are followed).

### Setup Overview
1) Domain MX server is set to Google (follow Workspace instructions, or start from having a working domain at Workspace already set up).
2) Start the procees of adding as domain to Proton Mail, and create the user@domain.com acccount within Proton mail.
3) Note the MX server settings for Proton Mail
4) In Google Workspace admin add the Proton Mail MX server under "Hosts"
5) In Google Workspace admin add the route to Proton mail for the desired user@domain.com under the "default routing" rules, using the MX server set in the previous step.
6) If you want to set a catch-all email to the user@domain.com account that you have moved to Proton Mail, you must set it within Google Workspace and NOT within Proton Mail, or else messages sent from Proton Mail to other @domain.com email address will not leave the Proton Mail server, and will just loop back to user@domain.com.


## Detailed Instructions

### Part 1: Setup Proton Mail Settings and Domain.com DNS Records

Following all Proton Mail setup instructions for the DNS on domain.com EXCEPT for DMARC (I'm still testing this) and MX server.

...in progress, screenshots pending. 
