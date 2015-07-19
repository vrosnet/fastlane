<h3 align="center">
  <a href="https://github.com/KrauseFx/fastlane">
    <img src="assets/fastlane.png" width="150" />
    <br />
    fastlane
  </a>
</h3>
<p align="center">
  <a href="https://github.com/KrauseFx/deliver">deliver</a> &bull; 
  <a href="https://github.com/KrauseFx/snapshot">snapshot</a> &bull; 
  <a href="https://github.com/KrauseFx/frameit">frameit</a> &bull; 
  <a href="https://github.com/KrauseFx/PEM">PEM</a> &bull; 
  <a href="https://github.com/KrauseFx/sigh">sigh</a> &bull; 
  <a href="https://github.com/KrauseFx/produce">produce</a> &bull; 
  <a href="https://github.com/KrauseFx/cert">cert</a> &bull; 
  <a href="https://github.com/KrauseFx/codes">codes</a>
</p>
-------

<p align="center">
  <img src="assets/deliver.png">
</p>

Pilot
============
[![Twitter: @KauseFx](https://img.shields.io/badge/contact-@KrauseFx-blue.svg?style=flat)](https://twitter.com/KrauseFx)
[![License](http://img.shields.io/badge/license-MIT-green.svg?style=flat)](https://github.com/fastlane/pilot/blob/master/LICENSE)
[![Gem](https://img.shields.io/gem/v/pilot.svg?style=flat)](http://rubygems.org/gems/pilot)


###### The unofficial TestFlight CLI

This tool allows you to manage all important features of Apple TestFlight using your terminal.

This includes

- Upload new builds and distribute them to all testers
- Set build information like changelog for new builds
- Add new testers to your team

Get in contact with the developer on Twitter: [@KrauseFx](https://twitter.com/KrauseFx)

-------
<p align="center">
    <a href="#installation">Installation</a> &bull; 
    <a href="#usage">Usage</a> &bull; 
    <a href="#tips">Tips</a> &bull; 
    <a href="#need-help">Need help?</a>
</p>

-------

<h5 align="center"><code>pilot</code> is part of <a href="https://fastlane.tools">fastlane</a>: connect all deployment tools into one streamlined workflow.</h5>

# Installation

    sudo gem install pilot

# Usage

For all commands you can specify the Apple ID to use using `-u felix@krausefx.com`. If you execute `pilot` in a project already using [fastlane](https://fastlane.tools) the username and app identifier will automatically be determined.

## Uploading builds

To upload a new build, just run 

```
pilot upload
```

This will automatically look for an `ipa` in your current directory and tries to fetch the login credentials from your [fastlane setup](https://fastlane.tools).

You'll be asked for any missing information. Additionally, you can pass all kinds of parameters to `pilot`:

```
pilot -u felix@krausefx.com
```

Additionally you can skip the submission of the binary, which means, the `ipa` file will only be uploaded and not distributet to testers:

```
pilot --skip_submission
```

`pilot` does all kinds of magic for you:

- Automatically detects the bundle identifier from your `ipa` file
- Automatically fetch the AppID of your app based on the bundle identifier

This gem uses [spaceship.airforce](https://spaceship.airforce) to submit the build metadata and iTunes Transporter to upload the binary :rocket:

## Managing beta testers

### List of Testers

This command will list all your testers, both internal and external.

```
pilot list
```

The output will look like this:

```
+--------+--------+--------------------------+-----------+
|                    Internal Testers                    |
+--------+--------+--------------------------+-----------+
| First  | Last   | Email                    | # Devices |
+--------+--------+--------------------------+-----------+
| Felix  | Krause | felix@krausefx.com       | 2         |
+--------+--------+--------------------------+-----------+

+-----------+---------+----------------------------+-----------+
|                       External Testers                       |
+-----------+---------+----------------------------+-----------+
| First     | Last    | Email                      | # Devices |
+-----------+---------+----------------------------+-----------+
| Max       | Manfred | email@email.com            | 0         |
| Detlef    | Müller  | detlef@krausefx.com        | 1         |
+-----------+---------+----------------------------+-----------+
```

### Add a new tester

To add a new tester to both your iTunes Connect account and to your app (if given), use the `pilot add` command. This will create a new tester (if necesssary) or add an existing tester to the app to test.

```
pilot add -e email@invite.com
```

Additionally you can specify the app identifier (if necessary): 

```
pilot add -e email@email.com -a com.krausefx.app
```

### Find a tester

To find a specific tester use

```
pilot find -e felix@krausefx.com
```

The resulting output will look like this:

```
+---------------------+---------------------+
|            felix@krausefx.com             |
+---------------------+---------------------+
| First name          | Felix               |
| Last name           | Krause              |
| Email               | felix@krausefx.com  |
| Latest Version      | 0.9.14 (23          |
| Latest Install Date | 03/28/15 19:00      |
| 2 Devices           | • iPhone 6, iOS 8.3 |
|                     | • iPhone 5, iOS 7.0 |
+---------------------+---------------------+
```

### Remove a tester

To remove an external tester:

```
pilot remove -e felix@krausefx.com
```

# Need help?
- If there is a technical problem with `pilot`, submit an issue.
- I'm available for contract work - drop me an email: pilot@krausefx.com

# License
This project is licensed under the terms of the MIT license. See the LICENSE file.

# Contributing

1. Create an issue to start a discussion about your idea
2. Fork it (https://github.com/fastlane/pilot/fork)
3. Create your feature branch (`git checkout -b my-new-feature`)
4. Commit your changes (`git commit -am 'Add some feature'`)
5. Push to the branch (`git push origin my-new-feature`)
6. Create a new Pull Request

