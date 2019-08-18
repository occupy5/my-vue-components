<template>
  <ul class="pagination" :class="paginationClass">
    <!-- 前一页 -->
    <li
      class="page-item prev-page"
      :class="{ disabled: value === 1, 'no-arrows': noArrows }"
    >
      <a class="page-link" aria-label="Previous" @click="prevPage">
        <template v-if="withText">
          上一页
        </template>
        <i class="fa-angle-double-left" v-else></i>
      </a>
    </li>
    <!-- 当前页面 -->
    <li
      class="page-item"
      v-for="item in range(minPage, maxPage)"
      :key="item"
      :class="{ active: value === item }"
    >
      <a class="page-link" @click="changePage(item)">{{ item }}</a>
    </li>
    <!-- 后一页 -->
    <li
      class="page-item next-page"
      :class="{ disabled: value === totalPages, 'no-arrows': noArrows }"
    >
      <a class="page-link" aria-label="Next" @click="nextPage">
        <template v-if="withText">
          下一页
        </template>
        <i class="fa-angle-double-right" v-else></i>
      </a>
    </li>
  </ul>
</template>
<script>
export default {
  name: "pagination",
  props: {
    type: {
      type: String,
      default: "primary",
      validator: value => {
        return [
          "default",
          "primary",
          "danger",
          "success",
          "warning",
          "info",
          "rose"
        ].includes(value);
      }
    },
    withText: Boolean,
    noArrows: Boolean,
    pageCount: {
      type: Number,
      default: 0
    },
    perPage: {
      type: Number,
      default: 5
    },
    total: {
      type: Number,
      default: 100
    },
    value: {
      type: Number,
      default: 1
    }
  },
  computed: {
    paginationClass() {
      return `pagination-${this.type}`;
    },
    totalPages() {
      if (this.pageCount > 0) return this.pageCount;
      if (this.total > 0) {
        return Math.ceil(this.total / this.perPage);
      }
      return 1;
    },
    pagesToDisplay() {
      if (this.totalPages > 0 && this.totalPages < this.defaultPagesToDisplay) {
        return this.totalPages;
      }
      return this.defaultPagesToDisplay;
    },
    minPage() {
      // 当前页码大于或等于页码显示总数
      if (this.value >= this.pagesToDisplay) {
        const pagesToAdd = Math.floor(this.pagesToDisplay / 2);
        const newMaxPage = pagesToAdd + this.value;
        if (newMaxPage > this.totalPages) {
          return this.totalPages - this.pagesToDisplay + 1;
        }
        return this.value - pagesToAdd;
      } else {
        // 当前页码小于页码显示总数时，minPage的值为1
        return 1;
      }
    },
    maxPage() {
      // 当前页码大于或等于页码显示总数时
      if (this.value >= this.pagesToDisplay) {
        // 增加的页码数
        const pagesToAdd = Math.floor(this.pagesToDisplay / 2);
        // 新的最大页码数
        const newMaxPage = pagesToAdd + this.value;
        if (newMaxPage < this.totalPages) {
          return newMaxPage;
        } else {
          // 到达尾页
          return this.totalPages;
        }
      } else {
        // 当前页码小于页码显示总数时
        return this.pagesToDisplay;
      }
    }
  },
  data() {
    return {
      defaultPagesToDisplay: 5
    };
  },
  methods: {
    range(min, max) {
      let arr = [];
      for (let i = min; i <= max; i++) {
        arr.push(i);
      }
      return arr;
    },
    changePage(item) {
      this.$emit("input", item);
    },
    nextPage() {
      if (this.value < this.totalPages) {
        this.$emit("input", this.value + 1);
      }
    },
    prevPage() {
      if (this.value > 1) {
        this.$emit("input", this.value - 1);
      }
    }
  },
  watch: {
    perPage() {
      this.$emit("input", 1);
    },
    total() {
      this.$emit("input", 1);
    }
  }
};
</script>
<style lang="scss" scoped>

@mixin shadow-4dp-color($color){
  box-shadow: 0 4px 5px 0 rgba($color, 0.14),
  0 1px 10px 0 rgba($color, 0.12),
  0 2px 4px -1px rgba($color, 0.2);
}
.page-link{
  position: relative;
  display: block;
  padding: .5rem .75rem;
  margin-left: 0;
  line-height: 1.25;
  color: #2196f3;
  background-color: transparent;
  border: 0 solid #dee2e6;
}

.no-arrows{
  display: none;
}

.noText{
  display: none;
}
.pagination{
  display: flex;
  padding-left: 0;
  list-style: none;
  border-radius: .25rem;

    > .page-item > .page-link,
    > .page-item > span{
        border: 0;
        border-radius: 30px !important;
        transition: all .3s;
        margin: 0 3px;
        padding: 0;
        min-width: 30px;
        height: 30px;
        line-height: 30px;
        color: #999999;
        font-weight: 500;
        font-size: 12px;
        text-transform: uppercase;
        background: transparent;
        text-align: center;
        cursor: pointer;

        &:hover,
        &:focus{
            color: #999999 !important;
        }
    }

    > .page-item.active > a,
    > .page-item.active > span{
        color: #999999;

        &,
        &:focus,
        &:hover{
            background-color: darken(#428bca, 6.5%);
            border-color: darken(#428bca, 6.5%);
            color: #fff !important;
            @include shadow-4dp-color(darken(#428bca, 6.5%));
        }

    }

    // Colors
    &.pagination-info{
        > .page-item.active > a,
        > .page-item.active > span{
            &,
            &:focus,
            &:hover{
                background-color:  #5bc0de;
                border-color:  #5bc0de;
                @include shadow-4dp-color(#5bc0de);
            }
        }
    }

    &.pagination-success{
        > .page-item.active > a,
        > .page-item.active > span{
            &,
            &:focus,
            &:hover{
                background-color: #5cb85c;
                border-color: #5cb85c;
                @include shadow-4dp-color(#5cb85c);
            }
        }
    }

    &.pagination-warning{
        > .page-item.active > a,
        > .page-item.active > span{
            &,
            &:focus,
            &:hover{
                background-color: #f0ad4e;
                border-color: #f0ad4e;
                @include shadow-4dp-color(#f0ad4e);
            }
        }
    }

    &.pagination-danger{
        > .page-item.active > a,
        > .page-item.active > span{
            &,
            &:focus,
            &:hover{
                background-color: #d9534f;
                border-color: #d9534f;
                @include shadow-4dp-color(#d9534f);
            }
        }
    }
}
</style>