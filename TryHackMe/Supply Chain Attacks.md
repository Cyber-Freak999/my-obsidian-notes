The vulnerability stemmed from a compromised access token of a developer with privileged access to the Lottie Player npm package repository. This allowed attackers to publish malicious versions of the `@lottiefiles/lottie-player` package. These versions included code that triggered crypto prompts, enabling attackers to gain unauthorised access to users' cryptocurrency wallets (if the victim connected their original wallet).  

## Affected Versions

The malicious versions of the Lottie Player package were:

- 2.05
- 2.06
- 2.07

## Impact

If an application integrated any of the compromised versions, users could see unexpected prompts to connect their cryptocurrency wallets. Attackers exploited this access to steal funds from connected wallets. In [one reported case](https://www.mitrade.com/insights/news/live-news/article-3-442401-20241031), a user lost an estimated $723,000 (10 BTC) due to unauthorised wallet access. 

## Technical Explanation

A typical deployment scenario involves a developer pushing code to a version control system (e.g., Git), which then updates the NPM registry. The NPM registry subsequently pushes the package to CDNs, which are deployed globally to serve files efficiently to browsers and web applications, as illustrated below.

![flow representing how code is pushed to CDNs](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1731521626182.png)  

In the case of the LottieFiles incident, no updates were made to the Git repository. Instead, a compromised developer access token was used to publish a modified package `@lottiefiles/lottie-player` directly to NPM, which then propagated to CDNs, impacting end-users.  

Execution of the script in a sandbox environment showed that once the user visits a page, it will show a popup, as shown below:

![Lottie crypto popup](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1731068611572.png)  

**Note**: Since the code modified by the attacker makes implicit calls to C2 and shares the user's information, it is not advised to execute it in any internet-connected environment.

When users click on any wallet, it asks them to connect their digital wallet.

![lottie connection with wallet QR code](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1731399521595.png)  

The vulnerable code makes a web socket connection to a domain `castleservices01[.]com`, which has previously been used in multiple crypto-phishing scams as well. The API call to the C2 server includes the **auth key**, **user browser details** and **local IP** for authentication/registration in the request parameters.

![inspect element in Chrome](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1731302663286.png)  

Below is the snippet of minified code added by the developer, which contains calls to crypto SDKs like wallet link, coin base, etc., which confirms that LottieFiles' original code has been modified.

```javascript
...
..
onClick:s},t))))}})),Em=u((e=>{"use strict";Object.defineProperty(e,"__esModule",{value:!0}),e.CBW_MOBILE_DEEPLINK_URL=e.WALLETLINK_URL=e.CB_KEYS_URL=void 0,e.CB_KEYS_URL="https://keys.coinbase.com/connect",e.WALLETLINK_URL="https://www.walletlink.org",e.CBW_MOBILE_DEEPLINK_URL="https://go.cb-w.com/walletlink"})),Cm=u((e=>{"use strict";Object.defineProperty(e,"__esModule",{value:!0}),e.WLMobileRelayUI=void 0;var t=_m(),r=Hp(),i=Em();e.WLMobileRelayUI=class{constructor(){this.attached=!1,this.redirectDialog=new t.RedirectDialog}attach(){if(this.attached)throw new Error("Coinbase Wallet SDK UI is already attached");this.redirectDialog.attach(),this.attached=!0}redirectToCoinbaseWallet(e){let t=new URL(i.CBW_MOBILE_DEEPLINK_URL);t.searchParams.append("redirect_url",(0,r.getLocation)().href),e&&t.searchParams.append("wl_url",e);let n=document.createElement("a");n.target="cbw-opener",n.href=t.href,n.rel="noreferrer noopener",n.click()}openCoinbaseWalletDeeplink(e){this.redirectDialog.present({title:"Redirecting to Coinbase Wallet...",buttonText:"Open",onButtonClick:()=>{this.redirectToCoinbaseWallet(e)}})
...
..
```

The above code is not easily detectable as malicious because it was served from a legitimate CDN service, which makes the supply chain attack particularly powerful, as it often goes unnoticed.  

If you're interested in examining the developer's code changes, you can view the differences between the original files by Lottie Player and the ones modified by the attackers. Start by opening the terminal and navigating to the code directory using the command `cd /home/ubuntu/Downloads/code`. Then, issue the command `kdiff3 lottie-player-2.04.min.js lottie-player-2.05.min.js`, which will open a window showing the differences between the original file (2.04) and the one modified by the hacker (2.05), as shown below:

![difference of files vulnerable and original file](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1731563169905.png)  

Note that the code has been minified and slightly encoded, making it harder for automated tools and security engineers to detect changes easily. This `diff` view helps in pinpointing specific modifications made to the code.