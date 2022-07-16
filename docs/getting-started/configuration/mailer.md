---
sidebar_position: 5
title: Mailer
---

# Mail Settings
Settings related to sending & receiving email. 

## New Email Templates
:::caution Beta Feature
The new email templates is currently in beta still under active devlopment. Some aspects of the feature may change in a future release
:::

The new email templates utilize a visual email editor through a thrid-party component [GrapesJS](https://grapesjs.com/). GrapesJS is still in active development. Currently two templates are avaliable with the new template format.

| Template | Description |
| --- | --- |
| Ticket-Created | Email sent when a new ticket is created|
| Password Reset | Email sent when a user requests a password reset on the Login Page |

## Mailer
SMTP settings to connect Trudesk Mailer to a provider for sending email. 
Not all email providers allow the same connection methods, Trudesk has been tested with the follow email providers.
- **GMail**
  - Requires Google Account to [Allow Less Secure Apps](https://support.google.com/accounts/answer/6010255?hl=en)
- **Office 365**
- **Exchang Server**
- **Outlook.com**
- **Zoho**

| Setting | Description |
| --- | --- |
| Mail Server | Server address for the SMTP host. |
| Port | Port for SMTP connection |
| Auth Username | Username for SMTP Authenication  |
| Auth Password | Password for SMTP Authenication | 
| From Address | From address used when sending mail. <br /> *Note: Most SMTP providers require the FROM address to match the Authenication user email address.* |
| Use SSLv3 | Enable SSLv3 if your SMTP provider requires it |

:::info Notice
You must **Apply** your settings before you can them with the **Test Settings** button.
:::

## Mail Check
The **Mail Check** process polls an IMAP inbox for new emails and ***tries*** to convert them into tickets. 

| Settings | Default | Description |
| --- | --- | --- |
| Mail Server | --- | IMAP Hostname or IP adress |
| Port | --- | Port used to connect to the IMAP server |
| Username | --- | Username of the IMAP mailbox to poll. |
| Password | --- | Password of the IMAP mailbox to poll. |
| Allow Self Signed Certificate | `disabled` | If the IMAP server utilize a self-signed cert, bypass validation checks. |
| Polling Interval | `10` | How often to poll the server for new messages in minutes.
| Create Account | `disabled` | If the user does not a trudesk account one will be created using their FROM email address |
| Delete Message | `disabled` | Once the message has been scanned, trudesk will delete the message from the imbox. <br />***Note: Trudesk will remove the message regardless if it was successfully processed. This will be addressed.*** |
| Default Ticket Type | `Issue` | All mail processed through the Mail Check process will have this ticket type. |
| Default Ticket Priority | `Normal` | All mail processed through the Mail Check will have this ticket priority |
