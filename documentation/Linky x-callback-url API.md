# Linky x-callback-url API

You can launch Linky from other apps using the [x-callback-url](http://x-callback-url.com) specification.

The registered URL scheme is `linky://`.

## Examples

**Examples using [Worflow](https://workflow.is)application:**

**Action for [Launch Center Pro](https://contrast.co/launch-center-pro/)** to open Linky and show the message composer with the URL contained in the clipboard and then return to Launch Center Pro when the message is sent. [❲Install action❳](https://launchcenterpro.com/br09kl)

```
linky://x-callback-url/open?url=clipboard&template=titleandurl&x-success={{launchpro://}}
```

**Safari or Chrome Bookmarklet** to launch Linky with the URL of the displayed page and then return to Safari or Chrome when the message is posted:

For Safari:

```
javascript:window.location='linky://x-callback-url/open?url='+encodeURIComponent(window.location)+'&x-success='+encodeURIComponent(window.location)
```

For Chrome:

```
javascript:window.location='linky://x-callback-url/open?url='+encodeURIComponent(window.location)+'&x-success=googlechrome%3A%2F%2F'
```

## URL format

The format for a URL action looks like this:

```
linky://x-callback-url/[action]?[action parameters]
```

There are 4 supported actions: `open`, `compose`, `parse` and `shorten`.

## /open

Open Linky with an url.

### Parameters

* **url** *[required]*

* An url, a text containing an url or `clipboard`.

* **accounts** *[optional]*

* The social profile account name.

* Multiple accounts can be specified by separating them by a comma. For ambiguous accounts, a suffix can be append: username *.twitter*, username *.mastodon*, username@instance *.mastodon*.

* Account names can be found in the App Settings > Accounts tab.

* **template** *[optional]*

* Defines the message template: `empty`, `url`, `title`, `titleandurl`, or `custom`.

* Add `+suggested_image` for adding the suggested image (if found) to the message.

* Use `custom` to define a custom message template (it must be used with `template-text` parameter).

* If not specified, the preference in the settings is used.

* **template-text** *[optional]*

* The value is a custom string defining the message template (set `template` parameter to `custom` ).

* Available placeholders: `{title}` for the web page title, and `{url}` for the web page url.

* **x-success** *[optional]*

* URL to open after the message is sent.

### Examples

Open apple.com:

```
linky://x-callback-url/open?url=[https://apple.com]
```

Open the url contained in the clipboard:

```
linky://x-callback-url/open?url=clipboard
```

Open an url and use a custom message template:

```
linky://x-callback-url/open?url=[https://www.theverge.com/2017/9/15/16314928/justin-hofman-seahorse-plastic-pollution-photography]&template=[custom+suggested_image]&template-text=[Must read 👀 {title} — {url} #sharedwithlinky]
```

Present the composer with @johndoe account:

```
linky://x-callback-url/open?url=[https://apple.com]&accounts=[johndoe]&action=composer
```

Cross-post a message using John Doe Twitter and Mastodon accounts:

```
linky://x-callback-url/open?url=[https://apple.com]&accounts=[johndoe.twitter,johndoe.mastodon]&action=composer
```

Open [Launch Center Pro](https://contrast.co/launch-center-pro/) app after sending the message:

```
linky://x-callback-url/open?url=[https://apple.com]&accounts=[johndoe]&action=composer&x-success=[launchpro://]
```

## /compose

Open the message composer with a text and an image.

### Parameters

* **text** *[optional]*

* Text of the message.

* **image-source** *[optional]*

* Add an image to the message: `none` (no image, default value), `clipboard` (image in the clipboard) or `base64` (see `image-data` parameter)

* **image-data** *[optional]*

* Base 64 encoded string from the image data (set `image-source` parameter to `base64` ).

* **accounts** *[optional]*

* The social profile account name.

* Multiple accounts can be specified by separating them by a comma. For ambiguous accounts, a suffix can be append: username *.twitter*, username *.mastodon*, username@instance *.mastodon*.

* Account names can be found in the App Settings > Accounts tab.

* **x-success** *[optional]*

* URL to open after the message is sent.

### Example

```
linky://x-callback-url/compose?text=[Hello World]&x-success=[sourceapp://]
```

## /parse

Parse an url and call the x-success callback URL with the `normalized_url` and `title` (web page title) parameters appended.

### Parameters

* **url** *[required]*

* An url, a text containing an url or `clipboard`.

* **ret_param_normalized_url** *[optional]*

* The return parameter for the normalized url will be named according to this value. If not specified, the parameter is named `normalized_url`.

* **ret_param_title** *[optional]*

* The return parameter for the title will be named according to this value. If not specified, the parameter is named `title`.

* **x-success** *[optional]*

* URL to open when the operation is complete.

* **x-error** *[optional]*

* Error domain is *com.pragmaticcode.linky.xcallback*. Possible error codes are `1` (Unsupported URL) or `2` (Bad server response).

### Example

```
linky://x-callback-url/parse?url=[https://apple.com]&x-success=[sourceapp://]
```

## /shorten

Shorten an url and call the x-success callback URL with the `short_url` parameter appended.

### Parameters

* **url** *[required]*

* An url, a text containing an url or `clipboard`.

* **service** *[optional]*

* The service name: `bitly`, `cloudapp`, `droplr`, `google` or `yourls`. If not specified, the account selected in the Settings is used.

* **destination** *[optional]*

* `url` (default value) or `clipboard`.

* **ret_param_short_url** *[optional]*

* The return parameter for the shortened url will be named according to this value. If not specified, the parameter is named `short_url`.

* **x-success** *[optional]*

* URL to open when the operation is complete.

* **x-error** *[optional]*

* Error domain is *com.pragmaticcode.linky.xcallback*. Possible error codes are `1` (Unsupported URL), `2` (Bad server response) or `3` (Account error).

### Example

```
linky://x-callback-url/shorten?url=[https://apple.com]&x-success=[sourceapp://]
```

[Linky x-callback-url API](https://www.pragmaticcode.com/linky/api/specs1-1.html) 
#documentation #social #automation