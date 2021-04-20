# Use safari inspect browser to improve iPhone layout

Shortly before I have been stuck on a rendering issue which only seems to happen on **iPhone**, this was so annoying when I was trying to debug it on my desktop computer – I simply can’t replicate the problem, so I found out a solution:

Apple have provided web developers with a quick and easy way to be able to debug and inspect elements on actual mobile devices (only iPhones and iPads currently) with their web browser Safari.

🍭 **this will only work on an actual Apple Mac, and not on Safari on Windows.**

Here are the steps I did:

- ( first go to iPhone settings > safari > advanced, enable webinformation )

- Plug in my iPhone

- Have Safari open on my iPhone, with the website open that I want to inspect element on.

- Open Safari on my Apple Mac, enable the Developer menu by going to `Safari > Preferences > Advanced` > Check the checkbox `“Show Develop menu in menu bar”`

- Now I have a `“Develop”` option in the top menu bar. Click on it, and I see my iPhone there as an option, hover over it and it shows the page I currently have open on Safari on my iPhone.

- Click the page, this will presented with a Web Inspector window for the page on my iPhone

- That's it! 🍷
