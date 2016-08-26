<template>
  <div class="form-horizontal">
    <div class="form-group">
      <div class="col-sm-6">
        <label>Date</label>
        <input
          type="date"
          class="form-control"
          v-model="timeEntry.date"
          placeholder="Date"
          />
      </div>
      <div class="col-sm-6">
        <label>Hours</label>
        <input
          type="number"
          class="form-control"
          v-model="timeEntry.totalTime"
          placeholder="Hours"
          />
      </div>
    </div>
    <div class="form-group">
      <div class="col-sm-12">
        <label>Comment</label>
        <input
          type="text"
          class="form-control"
          v-model="timeEntry.comment"
          placeholder="Comment"
          />
      </div>
    </div>
    <button class="btn btn-primary" @click="save()" v-link ="'/time-entries'">Save</button>
    <button v-link="'/time-entries'" class="btn btn-danger">Cancel</button>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        timeEntry: {
          user: {
            firstName: 'Chris',
            lastName: 'Nash',
            email: 'nash_web@outlook.com',
            image: 'http://nashwebdev.com/img/myFace.png'
          }
        }
      }
    },
    methods: {
      save () {
        let timeEntry = this.timeEntry
        this.$dispatch('timeUpdate', timeEntry)
        this.timeEntry = {}
      }
    }
  }
</script>
