<template>
  <ol class="breadcrumb">
    <li v-for="item in list"><span class="active" v-if="isLast($index)">{{item.label}}</span>
      <a v-link="{ name: item.link }" v-else>{{item.label}}</a>
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
      type: String,
      default: '/\00a0'
    }
  },

  ready () {
    this.$el.style.setProperty('--separator', this.separator)
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
  --separator: '/\00a0';

  list-style: none;
  align-items: center;
  display: flex;
  justify-content: flex-end;

  & > li + li:before {
    padding: 0 5px;
    color: #ccc;
    content: var(--separator);
  }
}
</style>
