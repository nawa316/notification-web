<template>
  <div class="relative w-screen flex">
    <div class="relative w-6/12 mx-auto h-screen bg-white shadow-lg px-12 py-10 overflow-auto">
      <!-- header -->
      <div class="flex justify-between mb-6 items-end">
        <div class="flex gap-1 items-center">
          <h1 class="font-bold text-lg">Notification</h1>
          <span class="px-2 bg-blue-900 text-white font-semibold rounded-md text-center">{{ notRead }}</span>
        </div>
        <span class="text-sm text-gray-500" @click="notifs = []">Mark all as read</span>
      </div>
      <div v-if="isNew" class="container1">
      <NewNotification @shareData="getDataFromChild" />
      </div>
      <!-- content -->
      <div class="flex gap-1 items-center">
        <!-- container notif -->
        <div class="flex flex-col gap-4 items-start" style="height: 400px;">
          <!-- notifikasi -->
          <div v-for="notif in notifs" :key="notif.id" class="flex gap-4 items-start">
            <!-- avatar -->
            <img v-if="notif.avatar" :src="notif.avatar" :alt="notif.name + ' avatar'" class="w-10">
            <!-- text -->
            <div v-if="notif.id">
              <p v-if="notif.action == 'Join'"><b>{{notif.name}}</b > has joined your group <b class="text-gray-600">Chese Club</b></p>
              <p v-else-if="notif.action == 'Follow'"><b>{{notif.name}}</b > has follow your group <b class="text-gray-600">Chese Club</b></p>
              <p v-else><b>{{notif.name}}</b > has send a message to <b class="text-gray-600">Chese Club</b></p>
              <div>
                <span v-if="realTime < notif.time + 1000" class="text-gray-500 text-sm cursor-pointer">{{ timeCategory[0] }}</span>
                <span v-else-if="realTime < notif.time + 5000" class="text-gray-500 text-sm cursor-pointer">{{ timeCategory[1] }}</span>
                <span v-else-if="realTime < notif.time + 6000" class="text-gray-500 text-sm cursor-pointer">{{ timeCategory[2] }}</span>
                <span v-else-if="realTime > notif.time + 6000" class="text-gray-500 text-sm cursor-pointer">{{ timeCategory[3] }}</span>
              </div>
              <div v-if="notif.hasRead" class="mt-2 w-3 h-3 rounded-full bg-red-500"></div>
              <div v-if="notif.action === 'Message'" class="border-2 border-gray-200 p-2 rounded-md mt-2">
                <p class="text-gray-700">{{notif.message}}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <button class="button1" @click="isNew = !isNew">
      Add New
    </button>
  </div>
</template>

<script>
import NewNotification from "./components/NewNotification.vue";
export default {
  name: 'NotificationPage',
  components: {
    NewNotification
  },
  data() {
    return {
      data: null,
      realTime: null,
      timeCategory:["just now","1 minutes ago","2 minutes ago","5 minutes ago", "long time ago"],
      isNew: false,
      notRead: 0,
      notifs: [],
      }
    },

  methods: {
    getDataFromChild(data) {
      const time = Date.now();
      const newNotif = {
        ...data,
        id: this.notifs.length + 1,
        time,
        hasRead: false,
      }
      this.notifs.push(newNotif);
      this.notRead++;
      this.isNew = false;
    },

    getRealTime(){
      const d = new Date()
      let time = d.getTime()
      this.realTime = time
    },


  mounted(){
    this.getRealTime()
  },
},
}
</script>

<style scoped>
.container1{
  display: flex;
  justify-content: center;
}

.button1{
  position: absolute;
  top: 80%;
  left: 90%;
  width: 100px;
  height: 100px;
  background-color: #fcbe24;
  border-radius: 100%;
  color: black;
  font-family: sans-serif;
  box-shadow: 5px 10px 8px #888888;
}
/* Tambahkan gaya CSS tambahan jika diperlukan */
</style>
