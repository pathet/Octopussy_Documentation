FAQ 
===

[How can I change the Logs Wizard messages limit ?](FAQ.md#how-can-i-change-the-logs-wizard-messages-limit-)

[How can I contribute to Octopussy Project ?](FAQ.md#how-can-i-contribute-to-octopussy-project-)

[How can I encrypt my syslog traffic ?](FAQ.md#how-can-i-encrypt_my_syslog-traffic-)

[How can I handle logs from files ?](FAQ.md#how-can-i-handle-logs-from-files-)

[How can I handle Windows Hosts ?](FAQ.md#how-can-i-handle-windows-hosts-)

[How can I login to Octopussy Web interface ?](FAQ.md#how-can-i-login-to-octopussy-web-interface-)

[How can I migrate Octopussy from one server to another one ?](https://github.com/sebthebert/Octopussy_Documentation/blob/master/FAQ.md#how-can-i-migrate-octopussy-from-one-server-to-another-one-)

[What are software requirements for Octopussy ?](FAQ.md#what-are-software-requirements-for-octopussy-)

[What is a Device in Octopussy ?](https://github.com/sebthebert/Octopussy_Documentation/blob/master/FAQ.md#what-is-a-device-in-octopussy-)

[What is a Message in Octopussy ?](FAQ.md#what-is-a-message-in-octopussy-)

[What is a Service in Octopussy ?](FAQ.md#what-is-a-service-in-octopussy-)

<hr>

### How can I change the Logs Wizard messages limit ?

You can change that limit by editing the parameter `wizard_max_msgs` in [/etc/aat/aat.xml](https://github.com/sebthebert/Octopussy/blob/master/etc/aat/aat.xml) file.

### How can I contribute to Octopussy Project ? 

Look at the Contribution section of the [Community page](http://www.octopussy.pm/community) on official website.

### How can I encrypt my syslog traffic ?

If you use rsyslog as your Octopussy logs source, you can [configure rsyslog to encrypt your syslog traffic with TLS](http://www.rsyslog.com/doc/rsyslog_tls.html).

### How can I handle logs from files ?

If you need to get logs from files, you can use the `asynchronous` Device Log Type.

Edit your Device configuration.

<p align="center">
  <img src="https://raw.githubusercontent.com/sebthebert/Octopussy_Documentation/master/img/Device%20page%20-%20Edit%20button.png" alt="Device page - Edit button"/>
</p>

Add a `Log Regexp` input and a `Syslog Output`.

<p align="center">
  <img src="https://raw.githubusercontent.com/sebthebert/Octopussy_Documentation/master/img/Device%20Log%20Type%20asynchronous.png" alt="Device Log Type asynchronous"/>
</p>

If your logs are already well formated (syslog with iso8601 datetime), 
you just need to match the whole line `^(.+)$` and rewrite the same line `__1__`.

If your log doesn't contain the Device name, you can use the `__device__` reserved word to add it.

### How can I handle Windows Hosts ?

You can use [Snare Agent for Windows](http://www.intersectalliance.com/projects/SnareWindows/) to send Windows logs to Octopussy.

Take a look at [Configuring Devices / Windows Host with Snare Agent](https://github.com/sebthebert/Octopussy_Documentation/blob/master/02_Configuring_Devices.md#windows-host-with-snare-agent) section.

### How can I login to Octopussy Web interface ?

The default URL is **https://\<your_server\>:8888/**.

The default **login / password** are **admin / admin**.

### How can I migrate Octopussy from one server to another one ?

If you want to migrate Octopussy from one server to another one, follow these 4 steps:
  * [Install Octopussy](https://github.com/sebthebert/Octopussy_Documentation/blob/master/01_Installation.md) on your new server
  * Copy Octopussy configuration from your old server to your new one
    * `scp -r /var/lib/octopussy/conf/ octopussy@new-octo-server:/var/lib/octopussy/`
  * [Configure your devices to send their logs](https://github.com/sebthebert/Octopussy_Documentation/blob/master/02_Configuring_Devices.md) to the new Octopussy server
  * Finally move your logs from your old server to the new one
    * `scp -r /var/lib/octopussy/logs/ octopussy@new-octo-server:/var/lib/octopussy/`

### What are software requirements for Octopussy ?

You can get the list of software requirements in [Installation / Standard Installation / Software Requirements](https://github.com/sebthebert/Octopussy_Documentation/blob/master/01_Installation.md#software-requirements) section.

### What is a Device in Octopussy ?

A Device is one source of syslog messages.
A Device can contains one or more Services.

### What is a Message in Octopussy ?

A Message is an object with 6 fields: 

  * `message id` this id is unique.
  * `pattern` this pattern is converted to regexp by **Octopussy Parser** to match syslog messages.
  * `logelevel` this level represents the criticity of the Message.
  * `taxonomy` it defines the category of the Message. (Auth, Network, System...)
  * `table` this table is used by **Octopussy Reporter** to generate Reports. 
  * `rank` this is the position of this Message in its Service.

### What is a Service in Octopussy ?

A Service is a collection of Messages.


----------------
TOFIX
### How can I configure Octopussy to interact with my LDAP/SMTP/Jabber server ? 

You can configure your LDAP/SMTP/Jabber server on the WebUI [[web#system configuration page|System Configuration Page]].

### How can I create a new Octopussy Plugin ?

Look at the [Plugin Howto](http://www.octopussy.pm/documentation/howtos/plugin) Page.

### How can I create a new Octopussy Service ? 

Look at the [New Service Creation](http://www.octopussy.pm/documentation/tutorials/new_service) tutorial.

### How can I see how many logs I received ?

You can see the number of syslog messages you received on the last minute on the WebUI [[web#main page|Main Page]].

### What is a Plugin in Octopussy ?

Look at the [Plugin Howto](http://www.octopussy.pm/documentation/howtos/plugin) Page.
