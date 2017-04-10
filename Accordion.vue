<!-- ACCORDION -->

<template>
    <nav :class="$style.accWrapper">
      <div :class="$style.accTitle" @click="toggleList">
        <span>{{ title }}</span>
        <img
          src="<!-- your chevron -->"
          alt="chevron"
          :class="[{ [$style.open_menu]: isDisplay, [$style.close_menu]: !isDisplay }, $style.accChevron]"
        />
      </div>
      <ul :class="[{ [$style.maxHeight]: isDisplay }, $style.accList]">
        <li :class="$style.accListItem" v-for="item in list">{{ item }}</li>
      </ul>
    </nav>
</template>

<script>

  export default {
      data () {
          return {
              isDisplay: false
          }
      },
      props: {
          title: {
            type: String,
            required: true
          },
          list: {
            type: Array,
            required: true
          },
          handlerClick: Function
      },
      methods: {
          toggleList () {
              this.isDisplay = !this.isDisplay
          }
      }
  }
  
</script>

<style lang="scss" module>

  .accWrapper {
    display:flex;
    flex-direction: column;
  }

  .accTitle {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    padding: 20px 0 15px;
    cursor: pointer;
  }

  .accChevron {
    width: 15px;
  }

  .accList{
    list-style: none;
    padding: 0;
    margin: 0;
    font-size: 16px;
    overflow: hidden;
    max-height: 0;
    transition: max-height .5s ease-out;
  }

  .accList.maxHeight {
    max-height: 500px;
    transition: max-height .5s ease-in;
  }

  .accListItem {
    font-size: 13px;
    margin: 4px 0;
  }

  /* chevron animation  */
  @keyframes open-menu {
    to {
      transform: rotate(90deg);
    }
  }

  @keyframes close-menu {
    from {
      transform: rotate(90deg);
    }
    to {
      transform: rotate(0deg);
    }
  }

  .open_menu {
    animation: open-menu 0.4s ease-out forwards;
  }

  .close_menu {
    animation: close-menu 0.4s ease-out forwards;
  }

</style>
