<template>
    <div class="container">
        <p>New Notification</p>
        <div class="form">
            <button :class="{'button-true': selectAction.selectFollow == true, 'button-false': selectAction.selectFollow == false}" @click="selectAction.selectFollow = !selectAction.selectFollow , notif.action = 'Follow'">Follow</button>
            <button :class="{'button-true': selectAction.selectJoin == true, 'button-false': selectAction.selectJoin == false}" @click="selectAction.selectJoin = !selectAction.selectJoin, notif.action = 'Join'">Join</button>
            <button :class="{'button-true': selectAction.selectMessage == true, 'button-false': selectAction.selectMessage == false}" @click="selectAction.selectMessage = !selectAction.selectMessage,notif.action = 'Message'">Message</button>
        </div>
        <div class="form">
            <p>Your name:</p>
            <input v-model="notif.name" placeholder="name"/>
        </div>
        <div class="form" v-if="selectAction.selectMessage">
            <p>Your message:</p>
            <input v-model="notif.message" placeholder="message"/>
        </div>
        <div class="form">
            <button class="button" @click="saveData, $emit('shareData', notif)">submit</button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'NewNotification',
  data() {
    return {
        name: null,
        message: null,
        isActive: false,
        selectAction:{
            selectFollow: false,
            selectJoin: false,
            selectMessage: false,
        },
        notif: {
            id: null,
            name: null,
            avatar: null,
            action: null,
            message: null, 
            time: null,
            hasRead: null,
        },
        }
    },
    methods:{
        saveData(){
            this.notif.name = this.name
            this.notif.message = this.message
        },
    }
};
</script>

<style scoped>
.container{
    display: flex;
    flex-direction: column;
    height: fit-content;
    width: 1000px;
    justify-content: center;
    align-items: center;
}

.form{
    padding: 20px;
}

.button-false{
    margin: 5px;
    padding: 10px;
    width: fit-content;
    height: fit-content;
    border-width: 1px;
    border-radius: 20px;
    border-color: black;
}

.button-true{
    margin: 5px;
    padding: 10px;
    width: fit-content;
    height: fit-content;
    border-width: 1px;
    border-radius: 20px;
    border-color: black;
    background-color: #fcbe24;
}
</style>