<!-- ACCORDION
a single component could be use as DROPDOWN MENU while a list of components is an ACCORDION MENU.

accTitle and accList heights are defined with max and min height to keep
the structure quite dynamic, so list can show n elements.

If a list could have a lot of items, accList max-height should be extended,
it dosen't affect on other accordion layouts but accList max-height should be close to the real
height to keep the best animation's perfomrmance -->

<template>
    <div class="col">
      <div :class="$style.accTitle" class="row-btw"  @click="toggleList">
        <span>{{ title }}</span>
        <MsmSvg
          :SvgIcoName="'chevron'"
          :class="[{ [$style.open_menu]: isDisplay, [$style.close_menu]: !isDisplay }, $style.accChevron]">
        </MsmSvg>
      </div>
      <ul :class="[{ [$style.maxHeight]: isDisplay }, $style.accList]">
        <li :class="$style.accListItem" v-for="item in list">{{ item }}</li>
      </ul>
    </div>
</template>

<script>
  import MsmSvg from 'library/Atoms/SVG/SVG'

  export default {
      data () {
          return {
              isDisplay: false
          }
      },
      props: {
          title: String,
          list: Array,
          handlerClick: Function
      },
      methods: {
          toggleList () {
              this.isDisplay = !this.isDisplay
          }
      },
      components: {
          MsmSvg
      }
  }
</script>

<style lang="scss" module>

  .accTitle {
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
