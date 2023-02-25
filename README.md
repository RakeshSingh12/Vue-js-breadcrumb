# Vue-js-breadcrumb
Vue breadcrumbs builds on the official vue-router package to provide simple breadcrumbs. This package is backwards compatible to support both Vue 1.x and Vue 2.x, with jest test case.

# Create Component :-

<template>
  <div>
    <h1>Area 1 - 2</h1>
    <router-link :to="{ name: 'Area1' }">Go to Area 1</router-link>
    <router-link :to="{ name: 'Area121' }">Go to Area 1 - 2 - 1</router-link>
    <router-link :to="{ name: 'Area2' }">Go to Area 2</router-link>
  </div>
</template>

<script>
export default {
  name: 'Area12',
  data () {
    return {}
  }
}
</script>

<style scoped>
a {
  margin: 0 10px;
}
</style>


# The Final Breadcrum.vue component :-

<template>
  <div class="breadcrumb">
    <ul>
      <li
        v-for="(breadcrumb, idx) in breadcrumbList"
        :key="idx"
        @click="routeTo(idx)"
        :class="{'linked': !!breadcrumb.link}">

        {{ breadcrumb.name }}

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Breadcrumb',
  data () {
    return {
      breadcrumbList: []
    }
  },
  mounted () { this.updateList() },
  watch: { '$route' () { this.updateList() } },
  methods: {
    routeTo (pRouteTo) {
      if (this.breadcrumbList[pRouteTo].link) this.$router.push(this.breadcrumbList[pRouteTo].link)
    },
    updateList () { this.breadcrumbList = this.$route.meta.breadcrumb }
  }
}
</script>

<style scoped>
  .breadcrumb {}
  ul {
    display: flex;
    justify-content: center;
    list-style-type: none;
    margin: 0;
    padding: 0;
  }

  ul > li {
    display: flex;
    float: left;
    height: 10px;
    width: auto;
    color: $default;
    font-weight: bold;
    font-size: .8em;
    cursor: default;
    align-items: center;
  }

  ul > li:not(:last-child)::after {
    content: '/';
    float: right;
    font-size: .8em;
    margin: 0 .5em;
    color: $light-default;
    cursor: default;
  }

  .linked {
    cursor: pointer;
    font-size: 1em;
    font-weight: normal;
  }
</style>


