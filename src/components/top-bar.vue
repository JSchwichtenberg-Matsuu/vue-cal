<template lang="pug">
  v-toolbar.top-bar(app light dense flat fixed align-center :class="{ scrolled: offsetTop > 104 }")
    v-toolbar-title.top-bar__title
      span.top-bar__title-line
      span.top-bar__title-line
      h1.primary--text.px-3
        a.top-bar__logo-link(href="#top" v-scroll-to="'#top'")
          .logo.top-bar__logo {{ todayDate < 10 ? `0${todayDate}` : todayDate }}
          div.top-bar__logo-title Vue Cal&nbsp;
        span.intro Vue.js full cal&nbsp; #[span.code --no-deps --no-bs]&nbsp; :metal:
    v-toolbar-items.top-bar__items
      v-menu(offset-y open-on-hover left attach transition="slide-y-transition")
        v-btn(flat color="secondary" slot="activator")
          v-icon.mr-2 school
          span Doc
        v-list.no-wrap
          v-list-tile(href="#installation" v-scroll-to="'#installation'") Installation
          v-list-tile(href="#how-to-use" v-scroll-to="'#how-to-use'") How To Use
          v-list-tile(href="#api" v-scroll-to="'#api'") API
          v-list-tile(href="#css-notes" v-scroll-to="'#css-notes'") CSS Notes
          v-list-tile(href="#release-notes" v-scroll-to="'#release-notes'") Release Notes
      v-menu(offset-y open-on-hover left attach transition="slide-y-transition")
        v-btn(flat color="secondary" slot="activator")
          v-icon.mr-2 apps
          span Examples
        v-list(dense).no-wrap
          v-list-tile(href="#ex--basic" v-scroll-to="'#ex--basic'") Basic, hide-weekends
          v-list-tile(href="#ex--small-cal" v-scroll-to="'#ex--small-cal'") Small calendar, hide view selector &amp; custom arrows
          v-list-tile(href="#ex--calendar-themes" v-scroll-to="'#ex--calendar-themes'") Calendar themes
          v-list-tile(href="#ex--internationalization" v-scroll-to="'#ex--internationalization'") Internationalization
          v-list-tile(href="#ex--timeline" v-scroll-to="'#ex--timeline'") Timeline
          v-list-tile(href="#ex--timeline-tweaking" v-scroll-to="'#ex--timeline-tweaking'") Timeline tweaking
          v-list-tile(href="#ex--today-current-time" v-scroll-to="'#ex--today-current-time'") Today's current time
          v-list-tile(href="#ex--disabled-views-and-calendar-events" v-scroll-to="'#ex--disabled-views-and-calendar-events'") Disable views &amp; calendar events
          v-list-tile(href="#ex--events-indicators-on-month-view" v-scroll-to="'#ex--events-indicators-on-month-view'") Events indicators on month view
          v-list-tile(href="#ex--custom-title" v-scroll-to="'#ex--custom-title'") Custom vue-cal title
          v-list-tile(href="#ex--timeless-events" v-scroll-to="'#ex--timeless-events'") Timeless Events
          v-list-tile(href="#ex--editable-deletable-events" v-scroll-to="'#ex--editable-deletable-events'") Editable / deletable events
          v-list-tile(href="#ex--overlapping-events" v-scroll-to="'#ex--overlapping-events'") Overlapping events
          v-list-tile(href="#ex--background-events" v-scroll-to="'#ex--background-events'") Background events
          v-list-tile(href="#ex--splitting-days" v-scroll-to="'#ex--splitting-days'") Splitting days
          v-list-tile(href="#ex--modifying-events-from-outside" v-scroll-to="'#ex--modifying-events-from-outside'") Modifying events from outside
          v-list-tile(href="#ex--emitted-events" v-scroll-to="'#ex--emitted-events'") Vue Cal emitted events
</template>

<script>
import Vue from 'vue'
import VueScrollTo from 'vue-scrollto'

Vue.use(VueScrollTo)

export default {
  props: {
    offsetTop: {
      type: Number,
      default: 0
    }
  },
  data: () => ({
    todayDate: (new Date()).getDate()
  })
}
</script>

<style lang="scss">
$primary: #42b983;
$secondary: #2c3e50;
$lighter-text: #ccc;

.top-bar {
  z-index: 10;
  position: absolute;
  background: linear-gradient(rgba(255, 255, 255, 0.7)) !important;
  border-bottom: 1px solid transparent !important;
  transition: 0.3s ease-in-out all, 0.1s 0s ease-in-out border-color;
  top: 0;

  .v-toolbar__content {
    padding: 0;
  }

  &__title {
    position: relative;
    overflow: visible;
    margin-left: auto !important;
    margin-right: auto !important;
    width: 15.5em;
    transition: 0.3s ease-in-out;
    font-size: 1em;
  }

  &__title-line {
    position: absolute;
    top: 50%;
    width: 130px;
    right: 100%;

    & + & {right: auto;left: 100%;}

    &:before, &:after {
      content: "";
      position: absolute;
      top: 0%;
      width: 100%;
      display: block;
      z-index: -1;
    }

    &:before {
      margin-top: -1px;
      border: 2px solid $primary;
    }

    &:after {
      margin-top: 5px;
      border: 1px solid $secondary;
    }
  }

  &__logo {
    position: relative;
    margin-right: 15px;
    vertical-align: middle;
    transition: 0.2s 0s ease-in-out;
    background-color: $primary;
    width: 38px;
    height: 36px;
    border-radius: 4px;
    display: inline-block;
    text-align: center;
    color: rgba(255, 255, 255, 0.7);
    opacity: 0.8;
    padding-top: 7px;
    font-family: impact, arial black, arial, sans-serif;
    transition: 0.4s 0.4s ease-in-out;
    transform: translate(3px, 3px) scale(0.9);
    box-shadow: 2px 2px 3px rgba(0, 0, 0, 0);

    &:before, &:after {
      content: '';
      position: absolute;
      top: 5px;
      width: 5px;
      height: 5px;
      background-color: #fff;
      border-radius: 5px;
      box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
    }

    &:before {left: 5px;}
    &:after {right: 5px;}

    .ready & {
      box-shadow: 2px 2px 3px rgba(0, 0, 0, 0.6);
      transform: translate(0, 0);
    }
  }

  &__logo-link {
    display: inline-block;
    background-color: rgba(255, 255, 255, 0.7);
  }

  &__logo-title {
    display: inline-block;
    vertical-align: middle;
    transition: 0.3s ease-in-out;
    font-size: 32px;
  }

  &__logo-title:after {
    content: "*";
    position: absolute;
    top: 0;
    margin-left: -7px;
    line-height: 1;
    opacity: 1;
    transition: opacity 0.3s ease-in-out;
  }

  .top-bar__items {
    position: absolute;
    right: 0;
    transition: 0.3s ease-in-out;
    transform: translateX(100%);
    opacity: 0;
    background-color: rgba(255, 255, 255, 0.7);
  }

  .top-bar__items .v-menu__content .v-list__tile {
    height: 30px;
    font-size: 1em;
    color: inherit !important;
  }

  .intro {
    position: absolute;
    top: 3.4em;
    left: 86px;
    color: #999;
    opacity: 1;
    transform: translateY(0em);
    transition: 0.3s .4s ease-in-out, 0s 0s top;
    font: 12px Roboto, Tahoma, Geneva, sans-serif;
    border: none;
    text-align: left;
  }

  .intro:before {
    content: "* ";
    vertical-align: super;
  }

  .intro em {
    padding-top: 3px;
    opacity: 0.6;
    transition: 0.3s;
  }

  .intro em:hover {
    opacity: 0.9;
  }

  &.scrolled {
    transition: 0.6s ease-in-out all, 0.3s 0.5s ease-in-out border-color;
    border-bottom-color: $lighter-text !important;
    position: fixed;

    & .top-bar__title {
      width: 100%;
    }

    & .top-bar__logo-title {
      font-size: 0.9em;
    }

    & .top-bar__logo-title:after {
      opacity: 0;
    }

    & .top-bar__items {
      transition: 0.3s 0.3s ease-in-out all;
      transform: translateX(0%);
      opacity: 1;
    }

    .intro {
      transition: 0.2s 0s ease-in-out all, 0s 0.3s top;
      transform: translateY(1em);
      opacity: 0;
      top: 5em;
    }
  }
}

@media screen and (max-width: 600px) {
  .scrolled .top-bar__logo {
    transform: scale(0.7);
    transform-origin: 50% 20%;
  }

  .top-bar.scrolled .v-toolbar__content,
  .scrolled .top-bar__logo-link {
    height: 32px !important;
  }
}

@media screen and (max-width: 449px) {
  .top-bar__items .v-btn {
    min-width: 50px;
    padding: 0 8px;
  }

  .top-bar__items a .v-btn__content span {
    display: none;
  }
}
</style>