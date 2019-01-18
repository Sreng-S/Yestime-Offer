<template>
  <div id="app">
    <!-- access root props via $root -->
    <h3>Images list: </h3>
    <div
      v-for="(img, k) in images"
    >
      <a
        :href="img"
        target="_blank"
        :key="k"
      >{{ img }}</a>
    </div>

    <h3>Redirect list: </h3>
    <div
      v-for="(rdt, k) in redirects"
      :key="k"
    >
      <a
        :href="rdt"
        target="_blank"
        :key="k"
      >{{ rdt }}</a>
    </div>
    <!--<router-view />-->
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: {
    width: {
      default: ''
    },
    height: {
      default: ''
    },
    type: {
      default: 'way-parking'
    },
    token: {
      default: ''
    },
    tagcount: {
      default: 5
    },
    format: {
      default: 'jpeg'
    },
    rank: {
      default: 0
    },
    eventid: {
      default: ''
    }
  },
  data () {
    return {
      dynamic_tag_all: 'https://yesti.me/api/v1/dynamic_tag_all?',
      images: [],
      redirects: [],
      tags: {}
    }
  },
  created () {
    const url = this.dynamic_tag_all + 'dimensions=' + this.$root.width + 'x' + this.$root.height + '&type=' + this.$root.type +
      '&token=' + this.$root.token + '&tagCount=' + this.$root.tagcount + '&format=' + this.$root.format
    axios
      .get(url)
      .then(response => {
        console.log(response.data)
        if (response.data.status === 'ok') {
          this.tags = response.data.tags
          this.tags.forEach(t => {
            let imageUrl, redirectUrl
            imageUrl = t.urls.image.replace('{event_id}', this.$root.eventid)
            this.images.push(imageUrl)
            redirectUrl = t.urls.redirect.replace('{event_id}', this.$root.eventid)
            this.redirects.push(redirectUrl)
          })
        }
        console.log(this.images)
        console.log(this.redirects)
      })
  },
  methods: {
  },
  watch: {
  }
}
</script>
