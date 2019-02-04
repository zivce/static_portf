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
## Client Dashboard

Client can get to the dashboard after signing in, and check for various features that this app provides. The client can buy tokens with Stripe integrated into the application. For the credit card info I've used **vue-stripe-elements-plus**, for card input so one can add the desired tokens. To disable the accidents of buying the tokens twice I've decided to put event modifer to the pay button, so that user can click only once. The tokens amount is stored into **vuex ** so component can instantly update the user menu with received tokens after Stripe has completed the transaction.

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

![token-charger](/img/token-charger.png "Purchasing tokens as client")

![user-dashboard](/img/info-user-menu-client.png "Client checking details of post job component")
