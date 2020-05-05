//система для відображення повідомлень
<template>
    <div class="message" v-if="messages.length>0">
        <p> Непрочитаних повідомлень: {{messages.length}} </p>
        <p> {{text}} </p>
        <input type="button" @click="close" value="Ок">
    </div>
</template>

<script>
import { mapState, mapGetters, mapMutations } from 'vuex';
export default {
    name:"messageSystem",
    data(){
        return{
        }
    },
    computed:{
        ...mapState(['messages']),
        ...mapGetters(['firstMessage','areSomeMessages','messagesCount'])
    },
    methods:{
       ...mapMutations(['removeMessage'])
    }
}
</script>
<style scoped>
    .message{
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        background: greenyellow;
        font: bold "Arial" 14px;
        padding: 10px;
        border: 1px solid green;
    }
</style>