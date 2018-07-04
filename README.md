# vue-picture

> A Vue Integrated [vue-preview](https://github.com/yuezm/vue-picture) Image Preview Plugin
## Requirements

[PhotoSwipe](https://github.com/dimsemenov/PhotoSwipe)

## Demo
    git clone https://github.com/yuezm/vue-picture.git
    open index.html in browser

## Usage

Notice:
 - **需要至少vue2.5以上版本**
 - **在vue-preview基础上,增加旋转功能**
 - **如果未传入w或者h,则宽高自适应**

```
-- app.js

import VuePicture from 'vue-picture'

 // defalut install
 Vue.use(VuePicture)

 // with parameters install
 Vue.use(preview, {
   mainClass: 'pswp--minimal--dark',
   barsSize: {top: 0, bottom: 0},
   captionEl: false,
   fullscreenEl: false,
   shareEl: false,
   bgOpacity: 0.85,
   tapToClose: true,
   tapToToggleControls: false
 })
```



```
-- template

    <template>
      <vue-picture :slides="slides" @close="handleClose"></vue-preview>
    </template>

    <script>

    export default {
        data () {
          return {
            slides: [
              {
                src: 'https://farm6.staticflickr.com/5591/15008867125_68a8ed88cc_b.jpg',
                msrc: 'https://farm6.staticflickr.com/5591/15008867125_68a8ed88cc_m.jpg',
                alt: 'picture1',
                title: 'Image Caption 1',
                w: 600,
                h: 400
              },
              {
                src: 'https://farm4.staticflickr.com/3902/14985871946_86abb8c56f_b.jpg',
                msrc: 'https://farm4.staticflickr.com/3902/14985871946_86abb8c56f_m.jpg',
                alt: 'picture2',
                title: 'Image Caption 2',
              }
            ]
          }
        },
        methods: {
          handleClose () {
            console.log('close event')
          }
        }
      }
    </script>
```