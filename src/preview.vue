<template>
  <div>
    <div class="my-gallery" itemscope itemtype="http://schema.org/ImageGallery">
      <template v-for="(item,key) in picList">
        <figure
          itemprop="associatedMedia"
          itemscope
          itemtype="http://schema.org/ImageObject" :key="key">
          <a :href="item.src" itemprop="contentUrl" :data-size="'' + item.w + 'x' + item.h">
            <img :src="item.msrc" :alt="item.alt" itemprop="thumbnail"/>
          </a>
          <figcaption style="display: none" itemprop="caption description">{{item.title}}</figcaption>
        </figure>
      </template>
    </div>
    <div class="pswp" tabindex="-1" role="dialog" aria-hidden="true" :class="classes">
      <div class="pswp__bg"></div>
      <div class="pswp__scroll-wrap">
        <div class="pswp__container">
          <div class="pswp__item"></div>
          <div class="pswp__item"></div>
          <div class="pswp__item"></div>
        </div>
        <div class="pswp__ui pswp__ui--hidden">

          <div class="pswp__top-bar">
            <div class="pswp__counter"></div>
            <button class="pswp__button pswp__button--close" title="Close (Esc)"></button>
            <button class="pswp__button pswp__button--share" title="Share"></button>
            <button class="pswp__button pswp__button--fs" title="Toggle fullscreen"></button>
            <button class="pswp__button pswp__button--zoom" title="Zoom in/out"></button>
            <button @click="rotate" class="pswp__button pswp__button--rotate" title="rotate /90deg"></button>
            <div class="pswp__preloader">
              <div class="pswp__preloader__icn">
                <div class="pswp__preloader__cut">
                  <div class="pswp__preloader__donut"></div>
                </div>
              </div>
            </div>
          </div>
          <div class="pswp__share-modal pswp__share-modal--hidden pswp__single-tap">
            <div class="pswp__share-tooltip"></div>
          </div>
          <button @click="rotateRelease" class="pswp__button pswp__button--arrow--left" title="Previous (arrow left)">
          </button>
          <button @click="rotateRelease" class="pswp__button pswp__button--arrow--right" title="Next (arrow right)">
          </button>
          <div class="pswp__caption">
            <div class="pswp__caption__center"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

window.deg = 0;
import 'photoswipe/dist/photoswipe.css';
import 'photoswipe/dist/default-skin/default-skin.css';

export default {
  name: 'preview',
  data() {
    return {
      picList: [],
    };
  },
  watch: {
    slides: function () {
      this.checkImage(this.slides);
    }
  },
  methods: {
    rotate() {
      window.deg = window.deg + 90;
      for (const item of document.querySelectorAll('.pswp__img')) {
        item.style.transform = `rotate(${window.deg}deg)`;
      }
    },

    rotateRelease() {
      window.deg = 0;
      for (const item of document.querySelectorAll('.pswp__img')) {
        item.style.transform = '';
      }
    },

    loadImage(url) {
      return new Promise((resolve, reject) => {
        const image = new Image();
        image.src = url;
        image.onload = () => {
          resolve(image);
        };

        image.onerror = () => {
          reject('获取图片错误');
        };
      });
    },

    checkImage(v) {
      for (const item of v || this.slides) {
        if (!('w' in item && 'h' in item)) {
          this.loadImage(item.src).then(image => {
            this.picList.push({
              w: image.width,
              h: image.height,
              src: item.src,
              msrc: item.msrc,
              alt: item.alt || '',
              title: item.title || '',
            });
          });
        }
      }
    }
  },

  created() {
    this.checkImage(this.slides);
  },
};
</script>
<style scoped>
  .pswp__button--rotate {
    background: url("./assert/img/rotate.png") center no-repeat;
  }

  .my-gallery {
    width: 100%;
  }

  .my-gallery img {
    width: 100%;
  }
</style>
