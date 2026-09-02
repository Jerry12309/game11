<template>
  <div class="bg-gradient-to-br from-purple-900 to-indigo-900 min-h-screen p-4">
    <div class="max-w-md mx-auto space-y-4">
      <div v-for="(item, idx) in list" :key="idx" class="bg-purple-100 rounded-2xl p-4 relative overflow-hidden">
        <div class="flex justify-between items-start">
          <span class="bg-purple-500 text-white px-2 py-1 rounded-lg text-sm">{{item.author}}</span>
          <span class="bg-orange-400 text-white px-2 py-1 rounded-lg text-sm">招募中</span>
        </div>
        <h2 class="text-2xl font-bold mt-2">{{item.gameName}}</h2>
        <p class="text-gray-600 text-sm">{{item.desc}}</p>
        <div class="flex items-center gap-3 mt-3 text-sm">
          <span>⏰ {{item.time}}</span>
          <span>👥 {{item.joinList.length}}/{{item.max}}</span>
        </div>
        <div class="flex gap-1 mt-2">
          <div v-for="u in item.joinList" :key="u" class="w-8 h-8 rounded-full bg-purple-400 text-white text-xs flex items-center justify-center">{{u.slice(0,1)}}</div>
        </div>
        <div class="flex gap-2 mt-3">
          <span class="bg-blue-400 text-white px-2 py-1 rounded text-xs">今日开局</span>
          <span v-if="item.max - item.joinList.length > 0" class="bg-orange-400 text-white px-2 py-1 rounded text-xs">差{{item.max - item.joinList.length}}人</span>
        </div>
        <img src="/images/avatar.jpg" class="absolute right-0 bottom-0 w-28 opacity-80 pointer-events-none" />
      </div>
    </div>

    <button @click="showForm = true" class="fixed bottom-6 left-1/2 -translate-x-1/2 bg-purple-600 text-white px-6 py-3 rounded-full text-lg shadow-lg">
      + 发起接龙
    </button>

    <div v-if="showForm" class="fixed inset-0 bg-black/60 flex items-center justify-center p-4">
      <div class="bg-white rounded-2xl p-4 max-w-md w-full">
        <h3 class="text-xl font-bold mb-3">创建约局</h3>
        <input v-model="form.author" placeholder="你的昵称" class="border w-full p-2 rounded mb-2"/>
        <input v-model="form.gameName" placeholder="游戏名称" class="border w-full p-2 rounded mb-2"/>
        <input v-model="form.desc" placeholder="简介" class="border w-full p-2 rounded mb-2"/>
        <input v-model="form.time" placeholder="开局时间" class="border w-full p-2 rounded mb-2"/>
        <input v-model.number="form.max" placeholder="最大人数" type="number" class="border w-full p-2 rounded mb-2"/>
        <div class="flex gap-2">
          <button @click="showForm=false" class="flex-1 py-2 border rounded">取消</button>
          <button @click="submit" class="flex-1 py-2 bg-purple-600 text-white rounded">提交创建</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const list = ref([])
const showForm = ref(false)
const form = ref({
  author:'',
  gameName:'',
  desc:'',
  time:'',
  max:4
})

const submit = ()=>{
  list.value.push({
    ...form.value,
    joinList:[]
  })
  showForm.value = false
  form.value = {author:'',gameName:'',desc:'',time:'',max:4}
}
</script>
