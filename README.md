# ChatbotAngular

In this lesson, we are going to build a chatbot in Angular from scratch using the Dialogflow conversation platform (formerly known as API.ai). Natural language processing (NLP) is one of the most challenging problems in machine learning. Over the past couple years, advances in large scale deep neural networks have made NLP technology available to the average developer.
In addition to Angular, you can deploy your bot to a wide variety of platforms with a single click - including Slack, Facebook Messenger, and many others.
This project is open source and can be found on github - Angular Chatbot.

angular chatbot demo with DialogFlow
Initial Setup Guide

Follow the steps below to get up and running quickly.
New Angular App from Scratch

For this tutorial, I will be starting a brand new Angular app from scratch. Make sure you are using v4.2 or later to take advantage of new Angular Animation features.
npm install -g @angular/cli
$ng new chatbot
$cd chatbot
Install Required Libraries

Our app has a only one extra dependency - the DialogFlow JavaScript SDK. It is written in TypeScript, so we can install it to the dev dependencies.
Currently, the SDK is still named api-ai, but I imagine this will change to dialogflow in the future. You can find the latest official SDKs here.

$npm install api-ai-javascript --save-dev
Fleshing out a Feature NgModule

We’re going to put all of our code into a feature module. This is a good practice in Angular to keep your code isolated and maintainable.
$ng g module chat
$ng g service chat -m chat
$ng g component chat/chat-dialog -m chat
The module should look like this. We only need to add the Angular FormsModule to the imports and add the ChatDialogComponent to exports.
/// chat.module.ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { ChatService } from '../chat.service';
import { ChatDialogComponent } from './chat-dialog/chat-dialog.component';


@NgModule({
  imports: [
    CommonModule,
    FormsModule
  ],
  declarations: [
    ChatDialogComponent
  ],
  exports: [ ChatDialogComponent ], // <-- export here
  providers: [ChatService]
})
export class ChatModule { }
Then import the chat module into the app module
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';

import { ChatModule } from './chat/chat.module';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    ChatModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
Now we have an isolated feature module that can be used in the main app.
You can also do this by loading the component with the Angular Router, but our app is not using routing for this example.

<!-- app.component -->
<chat-dialog></chat-dialog>
