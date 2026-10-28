# Design WhatsApp Web: real-time messaging, ordering, offline state and reconciliation

**Track:** Frontend system design  
**Level:** Hard  
**Time:** about 60 minutes  
**Reported at:** Microsoft, Salesforce

**[Design it on the whiteboard](https://frontend.nextjoblist.com/questions/design-whatsapp-web-real-time-messaging-ordering-offline)** and check yourself against the rubric: free, no account needed.

## Problem

Design the frontend of a WhatsApp Web–style messenger:

- a chat list with unread counts and last-message previews, and a conversation view with message history;
- sending and receiving messages in real time, with delivery states (sending, sent, delivered, read);
- correct ordering even when messages arrive late, out of order or twice;
- typing indicators and online presence;
- working offline: reading history, composing messages that are sent when the connection returns;
- multiple tabs and devices staying consistent.

Focus on the client: the real-time transport, the local data model, ordering and reconciliation, rendering long histories, and failure handling.

## Hints

<details><summary>Hint 1</summary>

Clarify scope first: one-to-one or group chats, history depth, how many devices per user, and what delivery states must be shown.

</details>

<details><summary>Hint 2</summary>

Centre the design on a local-first client store (memory plus IndexedDB) with an outbox, and a sync engine owning the WebSocket that resumes from a cursor after reconnect.

</details>

<details><summary>Hint 3</summary>

Expect pushback on ordering and duplicates (client ids, server sequence), reconnect gaps, multi-tab socket ownership, optimistic send failures, and rendering very long histories.

</details>

## Solution

The full answer is free on FrontendPro: [Design WhatsApp Web: real-time messaging, ordering, offline state and reconciliation](https://frontend.nextjoblist.com/questions/design-whatsapp-web-real-time-messaging-ordering-offline). It has a complete design walkthrough, the rubric interviewers score against, and follow-up questions with model answers.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20131%5D%20).
