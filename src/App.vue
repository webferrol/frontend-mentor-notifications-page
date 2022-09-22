<script setup lang="ts">
import { ref,computed } from "vue";
import TheNotification from "./components/TheNotification.vue";
import type {Notification} from "./components/TheNotification.vue";

//images
import angela from "./assets/images/avatar-angela-gray.webp";
import mark from "./assets/images/avatar-mark-webber.webp";
import jacob from "./assets/images/avatar-jacob-thompson.webp";
import rizky from "./assets/images/avatar-rizky-hasanuddin.webp";
import kimberly from "./assets/images/avatar-kimberly-smith.webp";
import nathan from "./assets/images/avatar-nathan-peterson.webp";
import anna from "./assets/images/avatar-anna-kim.webp";




const handleRead = () => {
  notifications.value.forEach(item=>item.read=true);
}

const markRead = (id:number) => {
  notifications.value[id-1].read = true;
}

const noRead = computed(():number=>notifications.value.filter(el=>el.read===false).length);
  
const notifications = ref<Notification[]>([
    {
      id: 1,
      author:'Mark Webber',
      imgSrc:mark,
      message:{
        messageServer: 'reacted to your recent post',
        notificationTitle: 'My first tournament today!',
      },
      date: '1m ago',
      read: false,
    },
    {
      id: 2,
      imgSrc:angela,
      author: 'Angela Gray',
      message: {
        messageServer: 'followed you'
      },
      date: '5m ago',
      read: false,
    },
    {
      id: 3,
      author:'Jacob Thompson',
      imgSrc: jacob,
      club:'Chess Club',
      message: {
        messageServer:'has joined your group'
      },
      date: '1 day ago',
      read: false,
    },
    {
      id: 4,
      imgSrc: rizky,
      author:'Rizky Hasanuddin',
      message: {
        messageServer: 'sent you a private message'
      },
      date: '5 days ago',
      messagePrivate:"Hello, thanks for setting up the Chess Club. I've been a member for a few weeks now and I'm already having lots of fun and improving my game.",
      read: true,
    },
    {
      id: 5,
      imgSrc: kimberly,
      author:'Kimberly Smith',
      message: {messageServer:'commented on your picture'},
      date: '1 week ago',
      read: false
    },
    {
      id: 6,
      imgSrc: rizky,
      author:'Rizky Hasanuddin',
      message: {
        messageServer: 'sent you a private message'
      },
      date: '5 days ago',
      messagePrivate:"Hello, thanks for setting up the Chess Club. I've been a member for a few weeks now and I'm already having lots of fun and improving my game.",
      read: false,
    },
    {
      id: 7,
      imgSrc: nathan,
      author:'Nathan Peterson',
      message: {
        messageServer:'reacted to your recent post',
        notificationTitle:'5 end-game strategies to increase your win rate'},
      date: ' 2 weeks ago',
      read: true,
    },
    {
      id: 8,
      imgSrc: anna,
      author:'Anna Kim',
      club:'Chess Club',
      message: {messageServer:'left the group'},
      date: ' 2 weeks ago',
      read: false
    },
  ]);
</script>

<template>
  <section class="container">
    <header class="main-header">
      <h1 class="main-header__title">Notifications <span class="badge">{{noRead}}</span></h1>
      <a href="#" @click.prevent="handleRead" class="main-header__mark-all">Mark all as read</a>
    </header>
    <section class="notifications">
      <TheNotification @markRead="markRead" v-for="item in notifications" :key="item.id" v-bind="item"></TheNotification>
    </section>
  </section>
</template>