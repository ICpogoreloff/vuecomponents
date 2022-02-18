<template>
  <div class="container pr-1">
    <div class="card">
      <h2>Актуальные новости {{ now }}</h2>
      <span>Открыто новостей: <strong>{{openRate}}</strong> | Прочитано новостей: <strong>{{readRate}}</strong></span>
    </div>
    <app-news
        v-for="item in news"
        :key="item.id"
        :title="item.title"
        :id="item.id"
        :is-open="item.isOpen"
        :was-read="item.wasRead"
        @open-news=" openNews"
        @read-news="readNews"
        @unmark="unreadNews"
    ></app-news>
  </div>
</template>

<script>
import AppNews from "@/components/AppNews"

export default {
  data() {
    return {
      now: new Date().toLocaleDateString(),
      openRate: 0,
      readRate: 0,
      news: [
        {
          title: 'Джо Байден чихнул на...',
          isOpen: false,
          id: 1,
          wasRead: false
        },
        {
          title: 'Жириновский раскритиковал...',
          isOpen: false,
          id: 2
        },
        {
          title: 'Секрет долголетия от Инстасамки...',
          isOpen: false,
          id: 3,
          wasRead: false
        }
      ]
    }
  },
  provide() {
    return {
      title: 'Список всех новостей',
      news: this.news
    }
  },
  methods: {
    openNews (data) {
      this.openRate++
      console.log(data)
    },
    readNews (id) {
      const idx = this.news.findIndex(news => news.id === id)
      this.news[idx].wasRead = true
      this.readRate++
      console.log('This id:', id)
    },
    unreadNews (id) {
      const news =this.news.find(news => news.id === id)
      news.wasRead = false
      this.readRate--
    }
  },

  components: {
    AppNews
  }
}
</script>

<style scoped>
h2 {
  color: darkred
}
app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
