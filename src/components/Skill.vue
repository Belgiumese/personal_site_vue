<template>
  <div class="skill">
    <div class="skillName">
      <span>{{ skill.name }}</span>
      <Tooltip v-if="skill.description" :text="skill.description" />
    </div>

    <div class="barGraph">
      <div
        v-for="(level, i) in skill.level"
        :key="i"
        class="bar"
        :class="{ glow: animateCount > i }"
      ></div>
    </div>
  </div>
</template>

<script>
import Tooltip from "@/components/Tooltip.vue";

export default {
  name: "Skill",

  components: {
    Tooltip
  },

  props: {
    skill: {
      type: Object,
      default() {
        return {
          name: "",
          level: 0
        };
      }
    },
    animate: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      animateCount: 0
    };
  },

  watch: {
    animate(newVal) {
      if (newVal) {
        const interval = setInterval(() => {
          if (this.animateCount >= this.skill.level) {
            clearTimeout(interval);
          }
          this.animateCount++;
        }, 200);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.skill {
  margin-bottom: 20px;
  text-align: left;

  .skillName {
    display: flex;
    align-items: center;
  }

  span {
    font-size: 17px;
    text-align: left;
    font-weight: 400;
  }

  .barGraph {
    font-size: 0;
    position: relative;
    text-align: left;
    height: 5px;
    margin-top: 10px;

    .bar {
      position: relative;
      top: -4px;
      width: 14.15%;
      background-color: #2b7a78;
      height: 5px;
      display: inline-block;
      border-radius: 8px;
      margin: 0 1.5%;
      opacity: 0;
      transition: opacity 1s ease-in-out, box-shadow 0.7s ease-in-out 1s;
      box-shadow: 0 0 7px 3px;

      &:first-of-type {
        margin-left: 0;
      }

      &:last-of-type {
        margin-right: 0;
      }

      &:nth-child(6) {
        background-color: #330968;
        color: #330968;
      }

      &:nth-child(5) {
        background-color: #322f7c;
        color: #322f7c;
      }

      &:nth-child(4) {
        background-color: #32538f;
        color: #32538f;
      }

      &:nth-child(3) {
        background-color: #316698;
        color: #316698;
      }

      &:nth-child(2) {
        background-color: #3192b0;
        color: #3192b0;
      }

      &:nth-child(1) {
        background-color: #30cdcf;
        color: #30cdcf;
      }

      &.glow {
        opacity: 100;
        box-shadow: none;
      }
    }
  }

  .info {
    font-size: 1.1em;
    color: rgba(0, 0, 0, 0.4);
    transition: all 0.2s ease-in-out;
    vertical-align: middle;
    margin-bottom: 5px;

    &:hover {
      color: rgba(0, 0, 0, 0.8);

      &::before,
      &::after {
        visibility: visible;
        opacity: 1;
        transform: translateX(5px) translateY(-50%);
      }
    }
  }

  span {
    position: relative;

    &::before {
      font-size: 15px;
      line-height: 20px;
      text-align: left;
      padding: 12px;
      border: 1px solid rgba(0, 0, 0, 0.3);
      width: 300px;
      border-radius: 3px;
      background: white;
      color: black;
      content: attr(data-info);
      position: absolute;
      opacity: 0;
      visibility: hidden;
      transition: all 0.16s ease-in-out;
      top: 50%;
      left: 140%;
      margin-left: 5px;
      transform: translateY(-50%);
      z-index: 90;
    }

    &::after {
      border: 10px solid transparent;
      width: 0;
      content: "";
      top: 50%;
      left: 120%;
      transform: translateY(-50%);
      border-right: 10px solid rgba(0, 0, 0, 0.3);
      border-left: none;
      position: absolute;
      opacity: 0;
      visibility: hidden;
      transition: all 0.16s ease-in-out;
    }
  }

  @keyframes glow {
    from {
      opacity: 0;
      box-shadow: 0 0 7px 3px;
    }

    to {
      opacity: 100;
    }
  }
}
</style>
