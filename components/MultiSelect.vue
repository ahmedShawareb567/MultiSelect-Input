<template lang="pug">
.multiSelect(:class="{'activeOptions': box.length}")
  h6.multiSelect-label(@click="toggleSelect()") {{label}}
  .multiSelect-main
    .multiSelect-bg(@click="toggleSelect()")
    .multiSelect-selectedItems(v-if="box && box.length")
        ul.p-0.m-0
          li.m-1(v-for="item in box" :key="item.value")
            span {{item.text}}
              small(@click="deleteOption(item.value)")
                svg.icon(xmlns='http://www.w3.org/2000/svg' height='24px' viewbox='0 0 24 24' width='24px' fill='#000000')
                  path(d='M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z')

        .multiSelect-selectedItems-arrows
          span(:class="{'activeArrow': isToggle}")
            svg.icon(xmlns='http://www.w3.org/2000/svg' height='24px' viewbox='0 0 24 24' width='24px' fill='#000000')
              path(d='M16.59 8.59L12 13.17 7.41 8.59 6 10l6 6 6-6z')

    .multiSelect-button
      .multiSelect-button-content(@click="toggleSelect()" v-if="!box.length")
        h6.mb-0 {{$t('choose')}}
        .multiSelect-button-arrows
          span(:class="{'activeArrow': isToggle}")
            svg.icon(xmlns='http://www.w3.org/2000/svg' height='24px' viewbox='0 0 24 24' width='24px' fill='#000000')
              path(d='M16.59 8.59L12 13.17 7.41 8.59 6 10l6 6 6-6z')

      .multiSelect-options(v-show="isToggle")

        .multiSelect-search
          input(type="text" v-model="search" :placeholder="placeholder" @keyup="searchEmitting()")

        .multiSelect-option(v-for="item in options" :key="item.value" :class="{'is-selected': box.includes(item)}")
          label.d-flex.align-items-center.mb-0(:for="`op-${item.value}`")
            div
              b-form-checkbox(v-model="box" :value="item" size="lg" :id="`op-${item.value}`" v-show="false")
              p.mb-0.ml-3 {{item.text}}
            .multiSelect-option-checkBox: span


</template>
<script>
export default {
  name: "MultiSelect",
  props: {
    vid: {
      type: String,
      default: null,
    },
    placeholder: {
      type: String,
      default: "Search ..",
    },
    value: {
      type: null,
      default: "",
    },
    label: {
      type: String,
      default: null,
    },
    type: {
      type: String,
      default: "text",
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      box: [],
      isToggle: false,
      isSelected: false,
      search: "",
    };
  },
  mounted() {
    this.box = this.value;

    window.addEventListener("click", (e) => {
      const select = document.querySelector(".multiSelect");
      if (!select.contains(e.target)) {
        this.isToggle = false;
      }
    });
  },
  methods: {
    toggleStyle() {
      this.isSelected = !this.isSelected;
    },
    deleteOption(id) {
      const findElementIndex = this.box.findIndex((i) => i.value == id);
      this.box.splice(findElementIndex, 1);
    },
    toggleSelect() {
      this.isToggle = !this.isToggle;
    },
    searchEmitting() {
      setTimeout(() => {
        this.$emit("searchChange", this.search);
      }, 200);
    },
  },
  watch: {
    value(val) {
      this.box = val;
    },
    box(newValue) {
      this.$emit("input", newValue);
    },
  },
};
</script>
<style lang="scss">
.multiSelect {
  user-select: none;
  &-search {
    margin: 0.5rem 0rem;
    input {
      width: 100%;
      border-radius: 3rem;
      height: 2rem;
      border: 0.1rem solid rgba(0, 0, 0, 0.2);
      padding-inline-start: 1rem;
      &:focus {
        outline-color: #ec255a;
      }
    }
  }
  .icon {
    transform: scale(0.8);
  }
  &.activeOptions {
    .multiSelect {
      &-options {
        top: 1rem;
      }
    }
  }
  &-bg {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0rem;
    left: 0rem;
  }
  &-label {
    font-size: 1rem;
    margin-bottom: 0.5rem;
  }
  &-main {
    position: relative;
    background-color: #fff;
    border: 0.1rem solid rgba(0, 0, 0, 0.2);
    border-radius: 0.5rem;
  }

  &-selectedItems {
    padding: 1rem 1rem 0.6rem 1rem;
    &-arrows {
      position: absolute;
      bottom: 0.3rem;
      right: 0.7rem;
      span {
        transition: all 0.2s ease-in-out;
      }
    }
    ul {
      list-style: none;
      li {
        display: inline-block;
        position: relative;
        border-radius: 1rem;
        background-color: #000;
        color: #fff;
        overflow: hidden;
        cursor: pointer;
        font-size: 0.9rem;
        span {
          position: relative;
          z-index: 99;
          padding: 0.4rem 0.7rem;
          small {
            position: absolute;
            top: 0rem;
            left: 0rem;
            width: 100%;
            height: 100%;
            background-color: #ec255a;
            border-radius: 0.5rem;
            color: #fff;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transition: opacity 0.2s ease-in-out;
            .icon {
              fill: #fff;
              transform: scale(0.7) !important;
            }
          }
        }
        &:hover {
          span {
            small {
              opacity: 1;
            }
          }
        }
      }
    }
  }
  &-button {
    position: relative;
    &-arrows {
      position: absolute;
      top: 0.3rem;
      right: 0.5rem;
      span {
        transition: all 0.2s ease-in-out;
      }
    }
    &-content {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0rem 1rem;
      height: 34.4px;
    }
  }
  &-options {
    position: absolute;
    top: 3rem;
    left: 0rem;
    width: 100%;
    padding: 0.5rem;
    z-index: 99;
    max-height: 15rem;
    overflow-y: auto;
    overflow-x: hidden;
    background-color: #fff;
    border-radius: 0.5rem;
    border: 0.1rem solid rgba(0, 0, 0, 0.2);
  }
  &-option {
    border-radius: 0.5rem;
    padding: 0.2rem 0.5rem;
    margin-bottom: 0.3rem;

    &-checkBox {
      width: 0.7rem;
      height: 0.7rem;
      border-radius: 50%;
      border: 0.1rem solid rgba(0, 0, 0, 0.1);
    }
    label {
      display: flex;
      align-items: center;
      justify-content: space-between;
      cursor: pointer;
    }
    &.is-selected {
      background-color: #eeeeeee5;
      .multiSelect {
        &-option {
          &-checkBox {
            background-color: #77d970;
            border-color: transparent;
          }
        }
      }
    }
  }
  &-error {
    font-size: 10px;
    margin-top: 0.3rem;
  }
}
.activeArrow {
  display: block;
  transform: rotate(-180deg);
}
[dir="rtl"] {
  .multiSelect {
    &-selectedItems {
      &-arrows {
        right: auto;
        left: 0.7rem;
      }
    }
    &-button {
      &-arrows {
        right: auto;
        left: 0.5rem;
      }
    }
  }
}
</style>
