<template>
   <div>
      <button
         v-if="$route.path !== '/time-entries/log-time'"
         v-link="'/time-entries/log-time'"
         class="btn btn-primary">
         Log Time
      </button>
      <div v-if="$route.path === '/time-entries/log-time'">
         <h3>Log Time</h3>
      </div>
      <hr />

      <router-view></router-view>

      <div class="time-entires">
         <p v-if="!timeEntries.length"><stong>No entries yet <i class="glyphicon glyphicon-warning-sign"></i></stong></p>
      </div>
      <div class="list-group">
         <a class="list-group-item" v-for="timeEntry in timeEntries">
            <div class="row">
               <div class="col-sm-2 user-details">
                  <img :src="timeEntry.user.image" class="avatar img-circle img-responsive" />
                  <p class="text-center">
                     <strong>
                        {{timeEntry.user.firstName}}
                        {{timeEntry.user.lastName}}
                     </strong>
                  </p>
               </div>
               <div class="col-sm-4">
                 {{timeEntry.comment}}
               </div>

               <div class="col-2-sm text-center time-block">
                  <h3 class="list-group-item-text total-time">
                     <i class="glyphicon glyphicon-time"></i>
                     {{timeEntry.totalTime}}
                  </h3>
                  <p class="label label-primary text-center">
                     <i class="glyphicon glyphicon-calendar"></i>
                     {{timeEntry.date}}
                  </p>
               </div>
               <div class="col-sm-1">
                  <button
                     class="btn btn-xs btn-danger delete-button"
                     @click="deleteTimeEntry(timeEntry)">
                     X
                  </button>
               </div>
            </div>
         </a>
      </div>
      <hr />
   </div>

</template>

<script>
   export default{
     data () {
       let existingEntry = {
         user: {
           firstName: 'Chris',
           lastName: 'Nash',
           email: 'nash_web@outlook.com',
           image: 'http://nashwebdev.com/img/myFace.png'
         },
         comment: 'First time entry',
         totalTime: 1.5,
         date: '2016-08-25'
       }
       return {
         timeEntries: [existingEntry]

       }
     },

     methods: {
       deleteTimeEntry (timeEntry) {
         let index = this.timeEntries.indexOf(timeEntry)
         if (window.confirm('Are you sure you want to delete this entry?')) {
           this.timeEntries.splice(index, 1)
           this.$dispatch('deleteTime', timeEntry)
         }
       }
     },
     events: {
       timeUpdate (timeEntry) {
         this.timeEntries.push(timeEntry)
         return true
       }
     }
   }
</script>

<style>
   .avatar{
      height: 75px;
      margin: 0 auto;
      margin-top: 10px;
      margin-bottom: 10px;
   }

   .user-details{
      background-color: #f5f5f5;
      border-right: 1px solid #ddd;
      margin: -10px 0;
   }

   .time-block{
      padding: 10px;
   }
   .comment-section{
      padding: 20px;
   }

   .split{
     border-bottom: 1px solid #ddd;
   }

</style>
