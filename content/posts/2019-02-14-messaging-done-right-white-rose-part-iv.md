---
layout: posts
title: Messaging done right! - White Rose - Part IV
linktitle: pentesting-project-part-iv
date: 2019-02-14T16:52:20.651Z
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
{{< img-shortcode imgurl="/img/client-inbox.png" >}}
{{< img-shortcode imgurl="/img/client-pentester-inbox.png" >}}

Messaging part is done with some Laravel logic and also some is done on the frontend. Message is sent to the backend but also added to binded array that is in data part of the component. Also after adding the message the input box is cleared immidately due to binding of that field to data.

```js
 bufferMsgForSending() {
      if (!this.one_msg.length) return;

      let new_msg = {
        // msg_id: this.msgs_for_send.length - 1,
        id: this.msg_send_id,
        client_to_pentester: false,
        pentester_to_client: true,
        date_time: moment().format("YYYY-MM-DD hh:mm:ss"),
        sender: this.user_name,
        message: this.one_msg,
        discusionID: this.whole_convo.discusion.id
      };

      this.client_msg_time = new_msg.date_time;

      this.one_msg = "";
      this.msg_send_id++;

      this.msgs_for_send.push(new_msg);

      ConvoSendMessagesAPI.sendMsg(new_msg);
    }
```

After the job has been posted and some pentester applies the conversation is started between them. Client can put reviews for job done by pentester and rate the pentester all in conversation tab. The job can be declined if client is not satisfied with what has been done.
{{< img-shortcode imgurl="/img/client-side-inbox-after-marked-as-completed.png" >}}

{{< img-shortcode imgurl="/img/client-reviewing-pentester.png" >}}
