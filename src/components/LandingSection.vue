<template>
  <Section
    id="home"
    class="container"
    :show-header="false"
    @mousemove.native="mousemove"
  >
    <ParticleCanvas ref="canvas" class="canvas" :is-active="isActive" />

    <Intersect :threshold="[0.8]" @enter="onEnter" @leave="onLeave">
      <div class="content">
        <div class="title">
          <Typer :text="'Hi, I\'m Aaron Coox'" />
          <h2 id="description">
            Computer & Electrical/Information Technology student. Welcome to my
            resume.
          </h2>
        </div>
        <div class="buttons">
          <a id="enterBtn" href="#about" @click="onClick($event)"
            >Explore Site</a
          >
          <a id="resumeBtn" href="/files/resume.pdf" target="_blank">
            <DownloadIcon /> Resume</a
          >
        </div>
      </div>
    </Intersect>
    <div id="overlay"></div>
  </Section>
</template>

<script>
import Intersect from "vue-intersect";
import Section from "./Section";
import Typer from "./Typer";
import ParticleCanvas from "./ParticleCanvas";
import { smoothScroll } from "../services/SmoothScroll";
import DownloadIcon from "../assets/icons/download.svg";

export default {
  name: "LandingSection",
  components: {
    Section,
    Typer,
    ParticleCanvas,
    Intersect,
    DownloadIcon
  },
  props: {
    isActive: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    onClick: smoothScroll,
    mousemove(evt) {
      this.$refs.canvas.mousemove(evt);
    },
    onEnter(evt) {
      this.$emit("enter", evt);
    },
    onLeave(evt) {
      this.$emit("leave", evt);
    }
  }
};
</script>
<style lang="scss" scoped>
@import "../styles/screenSizes.scss";

.container {
  position: relative;
  padding: 0;
  background-size: cover;
  background-attachment: fixed;
  width: 100%;
  height: 100vh;
  z-index: 1;

  .canvas {
    z-index: 3;
  }

  .content {
    z-index: 4;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    .title {
      width: 100%;
    }

    .title {
      display: block;
      text-align: center;
      z-index: 4;
      color: white;
    }

    .buttons a {
      display: inline-block;
      position: relative;
      text-align: center;
      z-index: 4;
      color: white;
      text-transform: uppercase;
      font-family: "Nunito Sans", Georgia, sans-serif;
      transition: 0.35s ease-in-out;
      line-height: 45px;
      text-decoration: none;
      border: 2px solid white;
      width: 150px;
      overflow: hidden;
      padding: 8px 2px;
      margin: 0 25px;

      &::before {
        transition: 0.35s ease-in-out;
        content: "";
        position: absolute;
        top: 0;
        right: -50px;
        bottom: 0;
        left: 0;
        border-right: 50px solid transparent;
        border-bottom: 70px solid rgba(255, 255, 255, 1);
        transform: translateX(-100%);
        z-index: -1;
      }

      &:hover {
        font-weight: bold;
        color: rgb(20, 20, 20);
        border-color: rgb(20, 20, 20);
        outline-color: rgb(20, 20, 20);

        &::before {
          transform: translateX(0);
        }
      }
    }

    #resumeBtn svg {
      position: relative;
      width: 20px;
      height: 20px;
      fill: currentColor;
      margin-right: 5px;
      top: 4px;
    }

    #description {
      font-family: "Nunito Sans", Georgia, sans-serif;
      font-weight: 200;
      font-size: 24px;
      display: inline-block;
      text-align: center;
      margin-top: 20px;
      margin-bottom: 60px;
      min-width: 10em;
      text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.7);
      width: 40%;
    }
  }

  #overlay {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background: linear-gradient(
      135deg,
      rgba(7, 18, 32, 0.75),
      rgba(15, 10, 34, 0.75)
    );
    z-index: 2;
  }
}

@include for-tablet-landscape {
  .container {
    .content {
      #description {
        width: 50%;
      }
    }

    .buttons a {
      margin: 15px;
    }
  }
}

@include for-tablet-portrait {
  .container {
    .content {
      #description {
        width: 65%;
        font-size: 22px;
      }

      .buttons a {
        margin: 10px;
      }
    }
  }
}

@include for-phone {
  .container {
    .content {
      #description {
        width: 85%;
        font-size: 20px;
        margin-top: 0;
        margin-bottom: 45px;
      }

      .buttons a {
        width: 140px;
        line-height: 40px;
      }
    }
  }
}

@include for-phone-small {
  .container {
    .content {
      .buttons a {
        width: 125px;
        line-height: 38px;
        font-size: 14px;
      }

      #resumeBtn svg {
        top: 2px;
        width: 17px;
        height: 17px;
      }
    }
  }
}
</style>

<style lang="scss">
@import "../styles/screenSizes.scss";

@media (max-width: 799px) {
  .webp .container {
    background-image: url("/img/background/background-mobile.webp");
  }

  .no-webp .container {
    background-image: url("/img/background/background-mobile.jpg");
  }
}

@media (min-width: 800px) {
  .webp .container {
    background-image: url("/img/background/background-1000.webp");
  }

  .no-webp .container {
    background-image: url("/img/background/background-1000.jpg");
  }
}

@media (min-width: 1100px) {
  .webp .container {
    background-image: url("/img/background/background-1400.webp");
  }

  .no-webp .container {
    background-image: url("/img/background/background-1400.jpg");
  }
}

@media (min-width: 1500px) {
  .webp .container {
    background-image: url("/img/background/background-1920.webp");
  }

  .no-webp .container {
    background-image: url("/img/background/background-1920.jpg");
  }
}

@include for-desktop-hd {
  .webp .container {
    background-image: url("/img/background/background-full.webp");
  }

  .no-webp .container {
    background-image: url("/img/background/background-full.jpg");
  }
}
</style>
