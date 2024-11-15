<template>
  <div class="carrousel-personnages">
    <div class="carrousel-personnages__container">
      <div class="carrousel-personnages__container__personnages">
        <div class="carrousel-personnages__container__personnages__main">
          <div class="carrousel-personnages__container__personnages__main__left" @click="animLeft">
          </div>
          <div class="carrousel-personnages__container__personnages__main__characters" >
            <div class="carrousel-personnages__container__personnages__main__characters__background" ref="background"></div>
            <img src="../assets/sprite1.png" ref="character0" alt="characters">
            <img src="../assets/sprite2.png" ref="character1" alt="characters">
            <img src="../assets/sprite3.png" ref="character2" alt="characters">
            <img src="../assets/sprite4.png" ref="character3" alt="characters">
          </div>
          <div class="carrousel-personnages__container__personnages__main__right" @click="animRight">
          </div>
        </div>
        <div class="carrousel-personnages__container__personnages__swipper">
          <span ref="swippe0"></span>
          <span ref="swippe1"></span>
          <span ref="swippe2"></span>
          <span ref="swippe3"></span>
        </div>
      </div>
      <div class="carrousel-personnages__container__description">
        <div class="carrousel-personnages__container__description__title">
          Des personnages<br> toujours aussi originaux
        </div>
        <div class="carrousel-personnages__container__description__subtitle">
          Offensives, défensives ou stratégiques, 19 classes que<br> vous ne verrez nul part ailleurs
        </div>
        <div class="carrousel-personnages__container__description__type">
          <div class="type-container">
            <div class="type-container__img" @mouseover="hoverType(0)" @mouseleave="unhoverType(0)" @click="changeFocus(0)">
              <img src="../assets/degats.png" alt="type">
              <img class="imgAnim" ref="type0" src="../assets/type0.png" alt="type" >
            </div>
            <div class="type-container__title">
              Dégâts
            </div>
          </div>
          <div class="type-container">
            <div class="type-container__img" @mouseover="hoverType(1)" @mouseleave="unhoverType(1)" @click="changeFocus(1)">
              <img src="../assets/soins.png" alt="type">
              <img class="imgAnim" ref="type1" src="../assets/type1.png" alt="type">
            </div>
            <div class="type-container__title">
              Soins
            </div>
          </div>
          <div class="type-container">
            <div class="type-container__img"  @mouseover="hoverType(2)" @mouseleave="unhoverType(2)" @click="changeFocus(2)">
              <img src="../assets/placement.png" alt="type">
              <img class="imgAnim" ref="type2" src="../assets/type2.png" alt="type">
            </div>
            <div class="type-container__title">
              Placement
            </div>
          </div>
          <div class="type-container">
            <div class="type-container__img"  @mouseover="hoverType(3)" @mouseleave="unhoverType(3)" @click="changeFocus(3)">
              <img src="../assets/tank.png" alt="type">
              <img class="imgAnim" ref="type3" src="../assets/type3.png" alt="type">
            </div>
            <div class="type-container__title">
              Tank
            </div>
          </div>

        </div>
        <div class="carrousel-personnages__container__description__link">
          <a class="button" href="#">Voir toutes les classes</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  name: 'CarrouselPersonnages',
  data() {
    return {
      carrousel: 0,
    }
  },
  mounted() {
    gsap.set(this.$refs.character0, { opacity: 1});
    gsap.set(this.$refs.swippe0, { background: "#fff"});
    gsap.set(this.$refs.type0, { opacity: 1});
    gsap.set(this.$refs.background, { background: `url(${require('@/assets/bg0.png')}) top center no-repeat`});
  },
  methods: {
    animRight() {
      this.actualCharacter = this.$refs[`character${this.carrousel}`];
      this.actualSwippe = this.$refs[`swippe${this.carrousel}`];
      this.actualType = this.$refs[`type${this.carrousel}`];
      if (this.carrousel === 3) {
        this.carrousel = 0;
      } else {
        this.carrousel++;
      }
      this.nextCharacter = this.$refs[`character${this.carrousel}`];
      this.nextSwippe = this.$refs[`swippe${this.carrousel}`];
      this.nextType = this.$refs[`type${this.carrousel}`];
      gsap.set(this.$refs.background, { background: `url(${require(`@/assets/bg${this.carrousel}.png`)}) top center no-repeat`});
      this.tl = gsap.timeline();
      this.tl
        .to(this.actualCharacter, {
          opacity: 0, 
        })
        .to(this.actualSwippe, {
          background: "#47413d", 
        }, "<")
        .to(this.nextCharacter, {
          opacity: 1, 
        }, "<")
        .to(this.nextSwippe, {
          background: "#fff", 
        }, "<")
        .to(this.actualType, {
          opacity: 0, 
        }, "<")
        .to(this.nextType, {
          opacity: 1, 
        }, "<")
    },
    animLeft() {
      this.actualCharacter = this.$refs[`character${this.carrousel}`];
      this.actualSwippe = this.$refs[`swippe${this.carrousel}`];
      this.actualType = this.$refs[`type${this.carrousel}`];
      if (this.carrousel === 0) {
        this.carrousel = 3;
      } else {
        this.carrousel--;
      }
      this.previousCharacter = this.$refs[`character${this.carrousel}`];
      this.nextSwippe = this.$refs[`swippe${this.carrousel}`];
      this.previousType = this.$refs[`type${this.carrousel}`];
      gsap.set(this.$refs.background, { background: `url(${require(`@/assets/bg${this.carrousel}.png`)}) top center no-repeat`});
      this.tl = gsap.timeline();
      this.tl
        .to(this.actualCharacter, {
          opacity: 0, 
        })
        .to(this.actualSwippe, {
          background: "#47413d", 
        }, "<")
        .to(this.previousCharacter, {
          opacity: 1, 
        }, "<")
        .to(this.nextSwippe, {
          background: "#fff", 
        }, "<")
        .to(this.actualType, {
          opacity: 0, 
        }, "<")
        .to(this.previousType, {
          opacity: 1, 
        }, "<")
    },
    hoverType(index) {
      if (index !== this.carrousel) {
        this.actualType = this.$refs[`type${index}`];
        gsap.to(this.actualType, {
          opacity: 1,
        });
      }
    },
    unhoverType(index) {
      if (index !== this.carrousel) {
        this.actualType = this.$refs[`type${index}`];
        gsap.to(this.actualType, {
          opacity: 0,
        });
      }
    },
    changeFocus(index) {
      console.log(index);
      console.log(this.carrousel);
      if (index === this.carrousel) return;
      this.actualCharacter = this.$refs[`character${this.carrousel}`];
      this.actualSwippe = this.$refs[`swippe${this.carrousel}`];
      this.actualType = this.$refs[`type${this.carrousel}`];
      this.nextCharacter = this.$refs[`character${index}`];
      this.nextSwippe = this.$refs[`swippe${index}`];
      this.nextType = this.$refs[`type${index}`];
      this.carrousel = index;
      gsap.set(this.$refs.background, { background: `url(${require(`@/assets/bg${this.carrousel}.png`)}) top center no-repeat`});
      this.tl = gsap.timeline();
      this.tl
        .to(this.actualCharacter, {
          opacity: 0, 
        })
        .to(this.actualSwippe, {
          background: "#47413d", 
        }, "<")
        .to(this.nextCharacter, {
          opacity: 1, 
        }, "<")
        .to(this.nextSwippe, {
          background: "#fff", 
        }, "<")
        .to(this.actualType, {
          opacity: 0, 
        }, "<")
        .to(this.nextType, {
          opacity: 1, 
        }, "<")
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "../css/variables.scss";

.carrousel-personnages {
  background: url(../assets/background.jpg) top center no-repeat;
  position: absolute;
  width: 100%;
  min-height: 760px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;

  &__container {
    display: flex;
    gap: 20px;
    box-sizing: border-box;
    justify-content: center;

    &__personnages {
      display: flex;
      flex-direction: column;
      gap: 20px;
      padding-top: 281px;

      &__main {
        display: flex;
        gap: 20px;
        align-items: center;

        &__left {
          background: url(../assets/arrow.png) center center no-repeat;
          width: 77px;
          height: 100px;
          transform: scale(0.9) rotateY(180deg);
          cursor: pointer;
          z-index: 1;
        }

        &__left:hover {
          transform: scale(1) rotateY(180deg);
        }

        &__characters {
          position: relative;
          top: 38px;
          width: 450px;
          height: 337px;
          &__background {
            content: " ";
            display: block;
            position: absolute;
            top: -318px;
            left: 50%;
            width: 1189px;
            height: 461px;
            transform: translateX(-50%);
            opacity: 1;
            transition: ease-in-out .2s;
          }
          img{
            position: absolute; 
            opacity: 0;
          }

        }

        &__right {
          background: url(../assets/arrow.png) center center no-repeat;
          transform: scale(0.9);
          width: 77px;
          height: 100px;
          cursor: pointer;
          z-index: 1;
        }

        &__right:hover {
          transform: scale(1);
        }
      }

      &__swipper {
        padding: 8px;
        background: rgba(0, 0, 0, 0.85);
        border-radius: 16px;
        line-height: 0;
        width: min-content;
        display: flex;
        left: 50%;
        transform: translateX(-50%);
        position: relative;
        top: 48px;

        span {
          width: 18px;
          height: 18px;
          border-radius: 50px;
          background: #47413d;
          opacity: 1;
          margin: 0 6px;
        }
      }
    }

    &__description {
      display: flex;
      flex-direction: column;
      gap: 24px;
      align-items: center;
      text-align: center;
      padding-top: 145px;
      box-sizing: border-box;
      position: relative;
      left: 36px;

      &__title {
        font-family: "Rowdies";
        text-transform: uppercase;
        font-size: 42px;
        line-height: 46px;
        color: #fff;
      }

      &__subtitle {
        font-family: "Lexend";
        font-size: 18px;
        font-weight: 400;
        color: #d6ccbd;
      }

      &__type {
        display: flex;
        justify-content: space-between;
        margin-bottom: 72px;
        padding-top: 0;
        gap: 15px;
        cursor: pointer;
      }

    }
  }
}

.type-container {
  display: flex;
  flex-direction: column;
  align-items: center;

  &__img{
    position: relative;
  }
  &__title {
    font-family: "Rowdies";
    text-transform: uppercase;
    font-size: 20px;
    color: #fff;
    position: relative;
    top: -13px;
  }
}

.imgAnim{
  position: absolute;
  left: 0;
  top: 0;
  opacity: 0;
  z-index: 1;
}

.button {
  text-shadow: none;
  font-family: "Rowdies";
  text-transform: uppercase;
  color: #fff;
  font-size: 30px;
  border-radius: 14px;
  background: #89b820;
  padding: 8px 34px;
  transition: all .3s ease;
}

.button:hover {
  filter: brightness(1.2);
  
}
</style>
