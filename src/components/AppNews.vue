<template>
  <div class="card">
    <h2>{{ title }}</h2>
    <app-button
        @action="open">
      {{isNewsOpen ? 'Закрыть' : 'Читать'}}
      </app-button>
    <app-button
        color="danger"
        v-if="wasRead"
        @action="unmark">
      Отметить непрочитанной
    </app-button>
    <div v-if="isNewsOpen">
      <hr />
    <p>Lorem ipsum dolor sit amet vero.</p>
    <app-button v-if="!wasRead" color="primary" @action="mark">
      Прочитать новость
    </app-button>

      <app-news-list></app-news-list>
    </div>
  </div>
</template>

<script>
import AppButton from "@/components/AppButton"
import AppNewsList from "@/components/AppNewsList"

export default {
  props: {
    wasRead: Boolean,
    title: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    },
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      validator(value) {
        console.log(value)
        return value === true || value === false
      }
    }
  },
  emits: {
    'open-news': null,
    'read-news' (id) {
      if (id) {
        return true
      }
      console.warn('Нет параметра ID для emit read-news')
      return false
    },
    unmark: null
  },
  data() {
    return {
      isNewsOpen: this.isOpen
    }
  },
  methods: {
    open () {
      this.isNewsOpen = !this.isNewsOpen
      if (this.isNewsOpen) {
        this.$emit('open-news', 42)
      }
    },
    mark () {
      this.isNewsOpen = false
      this.$emit('read-news', this.id)
    },
    unmark() {
      this.$emit('unmark', this.id)
    }
  },
  components: {
    AppButton,
    AppNewsList
  }
}
</script>

<style scoped>

</style>
