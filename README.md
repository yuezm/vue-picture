# vue-picture

> 一 A Vue Integrated [vue-preview](https://github.com/yuezm/vue-picture) Image Preview Plugin
> On the basis of the vue-preview, the image height and width adaptation is added,and the rotation has been added.
## Requirements

[PhotoSwipe](https://github.com/dimsemenov/PhotoSwipe)

## Demo
    git clone https://github.com/yuezm/vue-picture.git
    open index.html in browser

## Usage

Notice:
 - This plugin currently support vue2.5 and above


```
-- app.js

import VuePicture from 'vue-picture'

 // defalut install
 Vue.use(VuePicture)

 // with parameters install
 Vue.use(VuePicture, {
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

   **if the slides item has no w or h,then it will Adaptive**
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
                w: 1200,
                h: 900
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