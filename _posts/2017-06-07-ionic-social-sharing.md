---
layout: post
section-type: post
comments: true
title:  "Easy Social-Sharing with Ionic 3 and Ionic-native"
category: tutorial
tags: [ 'ionic','javascript','angular','ionic-3','web dev' ]
---

##### Have you integrated social sharing into your ionic app yet ?

If you answered no ,you should seriously consider it.
Social sharing is an apps integration with social media channels where the app shares information to services and feeds such as Twitter and Facebook.
 Social sharing has become a vital part of community building and brand marketing.
It can get more people talking about your app and increase your installs without your putting in any effort. You probably even you social-sharing with noticing it ,think about have many times have you seen and clicked these buttons

![image](/img/share.png)

We share everything articles , pictures , game play and game scores ,bible verses, playlists ,videos ,etc . As long as your app has something someone may find valuable and worth sharing to a friend , we should definitely give them a button to do it.

### Advantages of Social Sharing

* Social Influence : The more people that share from your app , the more people will become interested in it.
* Trusted Recommendations: People are more likely to download your App if its shared from someone they Trust
* Easy To Use : Letting your users share directly from the app is better than having them copy/paste or screenshot content.

## Implementation in Ionic 3

In this tutorial I will show your how to make app which implements social sharing with Ionic 3 and Ionic native. Ionic Native is a TypeScript wrapper for Cordova/PhoneGap plugins that make adding any native functionality you need to your Ionic mobile app easy.
The app we will create(shown below ) will retrieve quotes from an [external API](quotesondesign.com) and give users the ability to share the quotes they like.
![image](/img/social-final.png)

First lets create a new project using the ionic 3 -cli
```
ionic start socialsharing blank
```

Now we’re going to install Social Sharing native plugin. You can find the entire docs to the plugin in the ionic-native docs.
```
 ionic plugin add cordova-plugin-x-socialsharing
 npm install --save @ionic-native/social-sharing
```
To make the plugin work in our app will need to import it in `app.module.ts` so it’s available to be used throughout the app and also add it to the list of providers.
```javascript
import { SocialSharing } from '@ionic-native/social-sharing';

@NgModule({
 declarations: [...],
 imports: [...],
 bootstrap: [IonicApp],
 entryComponents: [...],
 providers: [
   ......,
   SocialSharing
 ]
})
export class AppModule {}
```

### NOW TO THE FUN STUFF !!!

To retrieve our quotes we will be using [Quotes on Design API](quotesondesign.com) ,this api returns an array of quotes objects with an ID , title (aurthor) ,content(quote) and a link. You can aslo specify the number of quotes you want.
Setting this up in ionic , head over to your `home.ts` file and add the following imports
```javascript
 // libraries for retrieving our quotes
import { Http } from '@angular/http'; // don't forget to import HttpModule in app.module.ts
import 'rxjs/add/operator/map';
import 'rxjs/add/operator/toPromise';
//library for social-sharing
import { SocialSharing } from '@ionic-native/social-sharing';
```
Now lets create our method for retrieving the quotes
``` javascript
export class HomePage {
  quotes :any;
  private  apiUrl :string = "http://quotesondesign.com/wp-json/posts?filter[orderby]=rand&filter[posts_per_page]=10"; //api url to retrieve 10 random quotes
  constructor(private http:Http, private socialSharing: SocialSharing ,public navCtrl: NavController) {
    this.getQuotes();
  }
  async getQuotes(){
          this.quotes = await this.http.get(this.apiUrl).map(res => res.json()).toPromise();;
    }
```
 The getQuotes methods uses a [async](https://hackernoon.com/6-reasons-why-javascripts-async-await-blows-promises-away-tutorial-c7ec10518dd9) to resolve the quotes API request and assigns that value to the quotes variable. The API returns an array of json objects containing our quotes.

 `Note: It is not advised to have http requests in your Component , best practise is to have all requests inside a provider. However for simplicity's sake the following code will suffice.`

### Sharing The quotes

Now that we actually have our quotes we need to create methods for sharing them.
In our app we will have four methods for sharing quotes.
![image](/img/sharebuttons.png)

1. General share : This method is going to open the share sheet and let our users share using the apps they have installed.
2. Whatsapp share: This method allows users to share the quote directly to whatsapp to a contact of their choose.
3. Facebook share : This method allows users to share a quote via the facebook app.
4. Twitter share : This method allows users to share a quote via the Twitter App.

These methods can text a `message` , a `file` and a `url` as arguments but for simplicity we will only be passing a message and setting the rest to null. You can read more on he plugin [here](https://ionicframework.com/docs/native/social-sharing/).

`Note : For method 2-4 , the respective apps must be installed in order to share a quote.`



The message we will share will be the quote ,its aurthor followed by the string "Sent from my Awesome App". To do this lets make a simple function compilemsg which takes in the index number of the quotes and returns a string containing the quote , the author and telling the user it was sent from our Awesome App.
```javascript
compilemsg(index):string{
  var msg = this.quotes[index].content + "-" + this.quotes[index].title ;
  return msg.concat(" \n Sent from my Awesome App !");
}
```
Now that we have our message , we can write functions for sharing it

#### Regular share

This will share the app via the action sheet to any app you choose.
```javascript
regularShare(index){
  var msg = this.compilemsg(index);
  this.socialSharing.share(msg, null, null, null);
}
```


#### Whatsapp share

This will share your message with your contacts or groups on whatsapp.
```javascript
whatsappShare(index){
  var msg  = this.compilemsg(index);
   this.socialSharing.shareViaWhatsApp(msg, null, null);
 }
 ```


#### Twitter share

This will share your message with the twitter app as a tweet or dm.
```javascript
twitterShare(index){
  var msg  = this.compilemsg(index);
  this.socialSharing.shareViaTwitter(msg, null, null);
}
```

#### Facebook share

 This will share your message via he facebook app.
 ```javascript
 facebookShare(index){
   var msg  = this.compilemsg(index);
    this.socialSharing.shareViaFacebook(msg, null, null);
  }
```

Now for our HTML

```html
  <!-- Header Bar -->
<ion-header>
  <ion-navbar>
    <ion-title>
      Social Sharing
    </ion-title>
  </ion-navbar>
</ion-header>

<ion-content padding>

  <!-- Cards containing quotes -->

  <ion-card *ngFor="let quote of quotes; let i = index;">

    <!-- Quote aurthor -->
    <ion-card-header>
      {{quote.title}}
    </ion-card-header>

    <!-- Quote Title -->
    <ion-card-content [innerHtml]=q uote.content></ion-card-content>

    <!-- Sharing Icons -->
    <ion-grid>
      <ion-row>
        <ion-col>
          <button ion-button icon-only (click)="regularShare(i)" color="primary" clear>
        <ion-icon class="share-icon" name="share"></ion-icon>
      </button>
        </ion-col>
        <ion-col>
          <button ion-button icon-only (click)="whatsappShare(i)" color="primary" clear>
        <ion-icon class="share-icon" name="logo-whatsapp"></ion-icon>
      </button>
        </ion-col>
        <ion-col>
          <button ion-button icon-only (click)="facebookShare(i)" color="primary" clear>
        <ion-icon  class="share-icon" name="logo-facebook"></ion-icon>
      </button>
        </ion-col>
        <ion-col>
          <button ion-button icon-only (click)="twitterShare(i)" color="primary" clear>
        <ion-icon class="share-icon" name="logo-twitter"></ion-icon>
      </button>
        </ion-col>

      </ion-row>
    </ion-grid>
  </ion-card>
</ion-content>
```
 And thats it , now our app is able share via the action share ,whatsapp , facebook and twitter.


### So we only get 10 quotes ??

 Our app currently suffers from one serious flaw , it only shows 10 quotes and there is no way of getting more. Tried of looking at the same ten quotes .Well whats the point of having a dynamic app if you just end up looking at the same static content.

 Let's fix that by adding Ionic's pull to refresh widget.In our `home.html` , lets add the following code just after our `ion-content` tag

 ```html
 <ion-refresher (ionRefresh)="doRefresh($event)">
   <ion-refresher-content pullingIcon="arrow-dropdown" pullingText="Pull to refresh" refreshingSpinner="bubbles" refreshingText="Refreshing...">
   </ion-refresher-content>
 </ion-refresher>

 ```
 This add an ion-refresher which updates our quotes when we pull the very top of the app by calling the doRefresh() method.
 Speaking of that ,lets head of to home.ts and add the doRefresh()  method.

  ```javascript
  doRefresh(refresher) {
    this.getQuotes();  // calls the getQuotes method

    setTimeout(() => {
      refresher.complete(); // stops the refresher 2 seconds after retreiving the Data
    }, 2000);
  }
   ```

   You can find the full code from this article on my [github repo](https://github.com/mikeyny/ionic-social-sharing-demo) .
