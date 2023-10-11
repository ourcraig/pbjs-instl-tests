# pbjs-instl-tests

This repository is for the testing of PBJS x GPT out-of-page interstitial integrations.

## Instructions

Observe behaviour on the test pages below. 

**Note:** GPT out-of-page interstitials have a frequency cap of 1 view per user per hour. To refresh the cap simply clear local storage on any test page:

```
localStorage.clear();
```

## Test Pages

[standard](https://ourcraig.github.io/pbjs-instl-tests/standard) - Renders a Prebid banner into a GPT interstitial slot using the default Prebid Universal Creative

**Notes:**
* The PUC renders the banner immediately when returned from GAM, despite not being viewable
* `pbjs.triggerBilling` is being used but no bid adapters seem to be using the `onBidBillable` event ([ref](https://github.com/search?q=repo%3Aprebid%2FPrebid.js+onBidBillable&type=code))
* The iframe containing the banner needs to be resized due to the 1x1 size of the PUC

[standard-sf](https://ourcraig.github.io/pbjs-instl-tests/standard-sf) - Attempts to render a Prebid banner into a GPT interstitial slot using the Prebid Universal Creative

**Notes:**
* The `pubUrl` in the PUC does not match the origin of the SafeFrame leading to CORS issues
* Cannot access the iframe inside the SafeFrame to resize for the 1x1 PUC due to CORS issues

[deferred-render](https://ourcraig.github.io/pbjs-instl-tests/deferred-render) - Defers rendering of a Prebid banner into a GPT interstitial slot using a modified Prebid Universal Creative

**Notes:**
* Requires an additional `hb_instl:true` ad-server targeting key
* If `hb_instl:true` is received then render happens on GPT impressionViewable event
* The iframe containing the banner needs to be resized due to the 1x1 size of the PUC

[deferred-render-sf](https://ourcraig.github.io/pbjs-instl-tests/deferred-render-sf) - Attempts to defer the render a Prebid banner into a GPT interstitial slot using a modified Prebid Universal Creative

**Notes:**
* Requires an additional `hb_instl:true` ad-server targeting key
* If `hb_instl:true` is received then `pubUrl` is set to `"*"`
* If `hb_instl:true` is received then render happens on GPT impressionViewable event
* `postMessage` from PUC does not seem to be able to reach parent window due to GPT SafeFrame inner iframe
* Cannot access the iframe inside the SafeFrame to resize for the 1x1 PUC due to CORS issues

## Documentation

* **Prebid.org** - [Interstitial Ads - PBJS](https://docs.prebid.org/features/InterstitialAds.html)
* **Developers.google.com** - [Display a web interstitial ad](https://developers.google.com/publisher-tag/samples/display-web-interstitial-ad)