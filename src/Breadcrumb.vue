<template>
  <ol class="breadcrumb">
    <li v-for="(item, index) in list"><span class="active" v-if="isLast(index)">{{ item.name }}</span>
      <a v-link="{ name: item.path }" v-else>{{ item.name }}</a>
    </li>
  </ol>
</template>

<script>
export default {

  props: {
    list: {
      type: Array,
      required: true,
      default: () => []
    },
    separator: {
      type: String
    }
  },

  ready () {
    if (this.separator) {
      this.$el.style.setProperty('--separator', `"${this.separator}"`)
    }
  },

  methods: {
    isLast (index) {
      return index === this.list.length - 1
    }
  }
}
</script>

<style lang="scss">
.breadcrumb {
  // > \003e
  // / \2044
  --separator: "\2044";

  list-style: none;
  align-items: center;
  display: flex;
  justify-content: flex-end;

  & > li + li:before {
    padding: 0 5px;
    color: #ccc;
    content: var(--separator, "\2044");
  }
}
</style>
