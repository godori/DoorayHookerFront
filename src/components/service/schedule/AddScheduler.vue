<template>
  <div class="col-xs-12 col-sm-4 col-md-4">
    <h1>Add Scheduler</h1>
    <div class="form-group">
      <label for="id">ID</label>
      <input type="text" name="id" v-model="schedule.id" placeholder="채팅방 ID"/>
    </div>
    <div class="form-group">
      <label for="description">Description</label>
      <input type="text" name="description" v-model="schedule.description" placeholder="봇에 대한 설명"/>
    </div>
    <div class="form-group">
      <label for="hookType">Hook Type</label>
      <select v-model="schedule.hookType" class="form-control">
        <option value="dooray-message">Message</option>
        <option value="dooray-culture">Culture Show Information</option>
        <option value="dooray-menu">Menu</option>
        <option value="dooray-commit">Github Today Commit</option>
      </select>
    </div>
    <div class="form-group" v-if="schedule.hookType === 'dooray-menu'">
      <label for="hookMenuType">Hook Menu Type</label>
      <select v-model="schedule.hookMenuType" class="form-control">
        <option value="lunch">Lunch</option>
        <option value="dinner">Dinner</option>
      </select>
    </div>
    <div class="form-group" v-if="schedule.hookType === 'dooray-commit'">
      <label for="githubIds">Github Ids</label>
      <input type="text" name="githubIds" v-model="schedule.githubIds" placeholder="jicjjang, godori, ..."/>
    </div>
    <div class="form-group" v-if="schedule.hookType === 'dooray-commit'">
      <label for="text">Message for committers</label>
      <input type="text" name="text" v-model="schedule.data.committer"  placeholder="Good job!">
    </div>
    <div class="form-group" v-if="schedule.hookType === 'dooray-commit'">
      <label for="text">Message for none committers</label>
      <input type="text" name="text" v-model="schedule.data.nonecommitter" placeholder="cheer up...">
    </div>
    <div class="form-group">
      <label for="imageUrl">Image Url</label>
      <input type="text" name="imageUrl" v-model="schedule.image" placeholder="봇 이미지 url"/>
    </div>
    <div class="form-group">
      <label for="hookTime">Hook Time</label>
      <input type="text" name="hookTime" v-model="schedule.hookTime" placeholder="09:00"/>
    </div>
    <div class="form-group">
      <label for="hookTerm">Hook Term</label>
      <!-- <input type="text" name="hookTerm" v-model="schedule.hookTerm" placeholder="주기"/> -->
      <select v-model="schedule.hookTerm" class="form-control">
        <option value="0">없음</option>
        <option value="5">5분</option>
        <option value="10">10분</option>
        <option value="15">15분</option>
        <option value="30">30분</option>
        <option value="60">1시간</option>
      </select>
    </div>
    <div class="form-group">
      <label for="name">Bot name</label>
      <input type="text" name="name" v-model="schedule.name" placeholder="봇 이름">
    </div>
    <div class="form-group">
      <label for="text">Bot Text</label>
      <input type="text" name="text" v-model="schedule.data.text" placeholder="내용">
    </div>
    <hr>
    <div class="form-group">
      <button class="btn btn-primary" @click="filteredSaveData">Submit</button>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  data: () => {
    return {
      schedule: {
        hookType: 'dooray-message',
        hookMenuType: 'lunch',
        id: '',
        description: '',
        githubIds: '',
        image: '',
        hookTime: '',
        hookTerm: '',
        name: '',
        data: {
          text: '',
          committer: '',
          nonecommitter: ''
          // ,
          // attachments: [
          //   {
          //     title: '',
          //     titleLink: '',
          //     text: '',
          //     color: ''
          //   }
          // ]
        }
      }
    }
  },
  methods: {
    ...mapActions([
      'saveData'
    ]),
    filteredSaveData () {
      if (this.schedule.id === 'url' || this.schedule.id === '') {
        alert('url 입력을 안함.')
      } else if (this.schedule.hookTime.length !== 5) {
        alert('시간은 02:00 같은 구조로 써주세요.')
      } else {
        this.schedule.image = decodeURIComponent(this.schedule.image)
        this.saveData(this.schedule)
      }
    }
  }
}
</script>

<style scoped>
  textarea {
    height: 320px;
  }

  button {
    margin-top: 10px;
  }
</style>
