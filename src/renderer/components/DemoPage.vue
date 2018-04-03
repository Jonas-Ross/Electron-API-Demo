<template>
    <div id="wrapper">
      <img id="logo" src="~@/assets/logo.png" alt="electron-vue">
      <main>
        <div class="left-side">
        <span class="title">
          Electron demos
        </span>
        </div>
        <div class="right-side">
          <div class="doc">
            <div class="title">Description</div><br/>
          </div>
        </div>

        <div class="left-side">
        <span class="title">
          Screen Information
        </span>
          <button class="alt" @click="showScreenSize()">Screen Information: {{screenSize}}</button>
        </div>
        <div class="right-side">
          <div class="doc">
            <div class="title">Electron Screen Module</div>
            <p>
              Electron provides and API for determining screen size. This can be useful if you have custom css that is responsive based on the size of the
              screen
            </p>
          </div>
        </div>

        <div class="left-side">
        <span class="title">Native Dialogs</span>
          <button class="alt" @click="showNativeDialog()">Information Dialogs</button><br/>
          <button class="alt" @click="showNativeErrorDialog()">Error Dialogs</button>
        </div>
        <div class="right-side">
          <div class="doc">
            <div class="title">Information Dialog</div>
            <p>
              With electron you can utilize native OS information dialogs, making your application look and feel closer to something natively
              programmed on that OS.
            </p>
          </div>
        </div>
      </main>
      <br/><br/>
      <router-link tag="button" :to="{name: 'landing-page'}">System Info</router-link>
    </div>
</template>

<script>
  export default {
    name: 'DemoPage',
    data() {
      return {
        screenSize: '',
      };
    },
    methods: {
      showScreenSize() {
        const {screen} = require('electron');
        this.screenSize = screen.getPrimaryDisplay().size
      },
      showNativeDialog() {
        const {dialog} = require('electron').remote
        dialog.showMessageBox({
          message: "This is a dialog",
        buttons: ["Neat!"]
        })
      },
      showNativeErrorDialog() {
        const {dialog} = require('electron').remote
        dialog.showErrorBox(
          "This is an error",
          "This is what an error looks like!"
        )
      },
    },
  };
</script>

<style scoped>

</style>