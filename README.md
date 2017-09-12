# minimalist-ripple-client

Access it online here: https://jatchili.github.io/minimalist-ripple-client

Or download the code here: https://raw.githubusercontent.com/jatchili/minimalist-ripple-client/master/index.html

**Note: Some users have reported bugs when using this client in Safari. Please use a non-Safari browser.**

Last updated: September 12, 2017.


## Contents

- [General](#general)
  - [What is this?](#what-is-this)
  - [You're asking for my secret key! Can I trust you?](#youre-asking-for-my-secret-key-can-i-trust-you)
- [How-to guide](#how-to-guide)
  - [Where is my secret stored? How it is transmitted?](#where-is-my-secret-stored-how-it-is-transmitted)
  - [Why are some buttons bold and others not?](#why-are-some-buttons-bold-and-others-not)
  - [What do all the buttons do under "identity"?](#what-do-all-the-buttons-do-under-identity)
  - [I get "account not found" when I try to do anything.](#i-get-account-not-found-when-i-try-to-do-anything)
  - [Under "account info", my "Balance" seems way too high to be correct.](#under-account-info-my-balance-seems-way-too-high-to-be-correct)
  - [How can I cancel an offer?](#how-can-i-cancel-an-offer)
  - [How can I use the btc2ripple outbound bridge?](#how-can-i-use-the-btc2ripple-outbound-bridge)
- [Contributing](#contributing)
  - [Are you going to keep updating this?](#are-you-going-to-keep-updating-this)
  - [How is the repo set up? Isn't it redundant to have `index.html` just being the same as `dev.html` with ripple-lib included inline?](#how-is-the-repo-set-up-isnt-it-redundant-to-have-indexhtml-just-being-the-same-as-devhtml-with-ripple-lib-included-inline)
  - [I want to add a feature or report a bug.](#i-want-to-add-a-feature-or-report-a-bug)
  - [Can you translate the interface into Chinese/Russian/whatever?](#can-you-translate-the-interface-into-chineserussianwhatever)
- [Miscellaneous](#miscellaneous)
  - [Why is this so ugly? Why does it violate every principle I learned in UI design class?](#why-is-this-so-ugly-why-does-it-violate-every-principle-i-learned-in-ui-design-class)
  - [Why don't you include this FAQ in the client itself?](#why-dont-you-include-this-faq-in-the-client-itself)
  - [Why not just include a link?](#why-not-just-include-a-link)



## General

### What is this?

This is a browser-based tool for interacting with the Ripple network. I assume you're familiar with how Ripple works. If not, take a look at the [Ripple wiki](https://wiki.ripple.com/Main_Page).

For more discussion, see the [thread on XRPTalk](https://xrptalk.org/topic/6792-minimalist-ripple-client/) or [on the Ripple Forum](https://forum.ripple.com/viewtopic.php?f=1&t=10446).


### You're asking for my secret key! Can I trust you?

We can make software more trustworthy either by making its components more trustworthy, or by eliminating as many components as possible. This client takes the latter approach.

What, then, do you still have to trust?

1. That GitHub will deliver the code faithfully (If you download it and run it locally, this is a one-time event)
2. That the SSL infrastructure is secure
3. That your computer/browser setup is trustworthy
4. That ripple-lib is trustworthy (Compare the code [included here](https://github.com/jatchili/minimalist-ripple-client/blob/master/index.html#L194-L205) with that [published by Ripple Labs](https://github.com/ripple/bower-ripple/blob/a734cc8484f7fa0aa97fbe22a23e3e6e68e7f044/ripple-min.js); you should find that they're identical)
5. That the code I wrote (~1600 lines) is trustworthy

Points #1-3 apply equally to any web application hosted on GitHub; #4 applies to any (such as RippleTrade) that uses ripple-lib. As for #5: I encourage you to read the code. If there's a backdoor in there, it'll very quickly be found.

Also: If I were trying to steal from you, I'm doing a really bad job of it. It's very easy to figure out what my real name is.


## How-to guide


### Where is my secret stored? How it is transmitted?

**Your secret is not stored anywhere** that persists once the window is closed\*. You ***MUST*** store it somewhere else - like in a text file and/or on paper - or else you'll lose access to your account!

Transactions are signed locally using ripple-lib. Assuming that ripple-lib is secure, your secret will never leave your computer.

\*Note: Depending on your browser, this may not be a cryptographically secure guarantee, since data might persist in memory even after the browser is closed. As a web developer I can't really do much about that. However, I can suggest that you use [Tor Browser](https://www.torproject.org/download/download), which does its best to clean up after itself on exit.


### Why are some buttons bold and others not?

The bold buttons signify "online" actions that communicate over the Internet, whereas the non-bold buttons do "offline" operations (like showing/hiding elements or performing cryptographic calculations). This makes it easy to know what the client is doing at any time. No online actions will occur unless you press a bold button.

(Note that the ~ buttons are bold, in case you couldn't tell.)


### What do all the buttons do under "identity"?

* set identity: Enter a secret where it says "secret", and click this button to load it. Now you can make transactions from this account.
* clear identity: Delete the currently-loaded key pair.
* generate identity: Make a new address/secret pair.
* rekey account: Issues you a new secret and invalidates the old one. This is useful if you believe your secret has been stolen, or if you want to secure control over an account that someone else has given you.
* encrypt secret: Once a secret is loaded, you can encrypt it with a passphrase to make it safer to store offline.


### I get "account not found" when I try to do anything.

Just because you've generated an identity, that doesn't mean Ripple actually knows about it yet. An account isn't "activated" until someone sends at least 20 XRP to it.


### Under "account info", my "Balance" seems way too high to be correct.

The Balance is listed in "drops", i.e. millionths of an XRP. Divide this number by 1,000,000 to find how much XRP you have. (Note that under the "send payment" and "trade" sections, XRP amounts should be entered as XRP, not as drops. Don't accidentally send a million times more than you intended!)


### How can I cancel an offer?

First, you need to be connected to Ripple, and you need to have loaded the secret for your account. Under "account details", click "use current identity", click "view/edit offers", find the offer in the table, and click "cancel" in that row.


### How can I use the btc2ripple outbound bridge?
 
Use this information at your own risk. It worked when I tried it, but that's no guarantee. I'm not affiliated with [btc2ripple](https://btc2ripple.com/#/), and they don't endorse me, nor I them.
 
1. Construct a URL from the following template: `https://btc2ripple.com/api/v1/bridge?type=quote&amount=BitcoinAmount%2FBTC&destination=BitcoinAddress` replacing `BitcoinAmount` with the amount of bitcoin you want to send (e.g. 0.123), and `BitcoinAddress` with the destination bitcoin address. (I think the amount is capped to 10 BTC per ripple account, but you should check the btc2ripple TOS to make sure.)
2. Load the URL in a browser window. You should get a response with a number of fields, the most important of which are `destination_address` (the ripple address you should send to), `destination_tag`, and `invoice_id`.
3. In Ripple, send a "Payment" transaction to the `destination_address`, setting the `destination_tag` and `invoice_id` fields accordingly. Make sure that the currency is BTC, and the amount is the same as the bitcoin amount you chose in step 1. You can use any path you like, as long as the received amount is correct. (Also, make sure to do this before the `expires` timestamp, which is 24 hours into the future.)
4. Wait for the bitcoin to arrive. (Mine posted to the blockchain in ~10 minutes, although the wait time may vary.)


## Contributing

### Are you going to keep updating this?

Only sporadically.

### How is the repo set up? Isn't it redundant to have `index.html` just being the same as `dev.html` with ripple-lib included inline?

The repo has two branches: `master` for development, and `gh-pages` for release. Submit pull-requests against `master`. Use `dev.html` for development, because it functions the same as `index.html` and doesn't have a huge block of minified JS to get in the way.

GitHub Pages requires that there be a file called `index.html` in the root directory, which is the file you see when you [access it online](https://jatchili.github.io/minimalist-ripple-client). We want this file not to reference any external resources, so that people can download and run it easily.


### I want to add a feature or report a bug.

You can give feedback on the [forum thread](https://xrptalk.org/topic/6792-minimalist-ripple-client/), create an issue, or make a pull-request.


### Can you translate the interface into Chinese/Russian/whatever?

I can't, but you can! If there's enough demand for another language, then it may be worth doing. Comment on the [forum thread](https://xrptalk.org/topic/6792-minimalist-ripple-client/) and we can figure it out.


## Miscellaneous

### Why is this so ugly? Why does it violate every principle I learned in UI design class?

This client isn't designed to be pretty, or usable. It's supposed to be *small*. Besides, unstyled `<h2>` and `<button>` elements have a certain quaint charm to them, don't they?

### Why don't you include this FAQ in the client itself?

Because then it wouldn't be minimalist.

### Why not just include a link?

What if I move the FAQ somewhere else? If the client gets translated, do I have to translate this page also? What if someone is running it locally and accidentally clicks the link, thereby revealing their IP address to GitHub? So much to think about...
