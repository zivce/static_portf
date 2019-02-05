---
layout: posts
title: White Rose - Part III
linktitle: pentesting-project-part-iii
date: 2019-02-04T13:43:06.821Z
tags:
  - vue
  - laravel
  - trello
  - ethical hacking
  - vuex
  - vue-router
  - apache
  - mysql
categories:
  - DEVELOPMENT
---
Client can get to the dashboard after signing in, and check for various features that this app provides. The client can buy tokens with Stripe integrated into the application. For the credit card info I've used **vue-stripe-elements-plus**, for card input so one can add the desired tokens. To disable the accidents of buying the tokens twice I've decided to put event modifer to the pay button, so that user can click only once. 

```
pay() {
     this.$validator.validateAll().then(isFormOk => {
       // used vee-validate for form validation
       // this complete is that it is valid card input
       if (isFormOk && this.complete && this.completeform) {
         createToken().then(token => {
           let tokens_already = this.$store.returnTokens;
           let tk = this.prop.value;
           this.$store.commit("setTokens", { tokens: tk });
           this.notifySuccess("Tokens added.", "Success");
           TokenChargerAPI.sendTokenAndAmount(token, this.prop.value);
         });
       } else this.errorToast("Please fill out the form", "Error!");
     });
   }
 }
```


{{< img-shortcode imgurl="/img/info-user-menu-client.png" >}}

The tokens amount is stored into **vuex** so component can instantly update the user menu with received tokens after Stripe has completed the transaction. For Stripe to function properly it is needed to put security token and amount and send it to the back-end. After transaction completes the tokens will be added to the balance of user and he can proceed to adding a new job if he navigates to post job component of application.

{{< img-shortcode imgurl="/img/token-charger.png" >}}

{{< img-shortcode imgurl="/img/token_purchase_success.png" >}}

## Brief user details

User can navigate from the left side menu, to the brief details component, where he can check out what is current state of his account. Information shown is state of jobs, how many jobs are finished so far, how many jobs are started and how many are there in general. User can navigate to inbox, jobs, sites section by clicking on the icons. More about jobs, inbox and sites section in next post. 

{{< img-shortcode imgurl="/img/profile-page.png" >}}
