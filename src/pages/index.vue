<script>
export default {
  data() {
    return {
      windowWebview: undefined,
      currentWebview: undefined
    }
  },
  methods: {
    async getCurrentWindowWebView() {
      let pages = getCurrentPages();
      const thisPage = pages[pages.length - 1];
      this.windowWebview = thisPage.$getAppWebview()
    },
    async createWebView() {
      this.currentWebview = plus.webview.create('https://arco.design/vue/start', 'default2333', {
        width: '100%',
        bounce: 'vertical',
        userSelect: true,
        cachemode: 'cacheElseNetwork',
        hardwareAccelerated: true,
        plusrequire: 'ahead',//当这个值为ahead时，就会导致与appendJsFile方法一起造成策略失效
        videoFullscreen: 'landscape-primary',
        errorPage: '_www/static/app/html/error/error01.html',
        progress: {
          color: '#4580ee',
          height: '2px'
        },
        scalable: true,
      })
      this.currentWebview.appendJsFile('_www/static/app/test.js')//本来打算的是在这里加载js文件
      this.currentWebview.show()
      this.windowWebview.append(this.currentWebview)
    }
  },
  async onReady() {
    await this.getCurrentWindowWebView()
    await this.createWebView()
  }
}
</script>

<template>
  <AppLogos />
  <InputEntry />
</template>

<style></style>

<route type="home" lang="json">{}</route>
