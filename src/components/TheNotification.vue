
<script setup lang="ts">
export interface Message {
    messageServer: string;
    notificationTitle?: string;
}

export interface Notification {
    id: number;
    author: string;
    imgSrc: string;
    message: Message;
    date: string;
    messagePrivate?: string;
    club?: string;
    read: boolean;
}
withDefaults(defineProps<Notification>(), {
    author: '',
    text: '',
    date: '',
});
</script>
<template>
    <div class="notification" :class="{'notification--unread':!read}">
        <img class="notification__img" :src="imgSrc" :alt="author">
        <div class="notification__message">
            <div class="message__content"
                style="display: flex; align-items: center;flex-wrap: wrap; column-gap: .2rem;">
                <strong>{{author}}</strong>
                <span class="text-server">{{message.messageServer}}</span>
                <span class="text-club">{{club}}</span>
                <em class="text-notification-title">{{message?.notificationTitle}}</em>
                <span @click="$emit('markRead',id)" class="text-unread" v-if="!read">No leído</span>
            </div>
            <span class="message__date">{{date}}</span>
            <div class="message__private" v-if="messagePrivate">
                {{messagePrivate}}
            </div>
        </div>
    </div>
</template>