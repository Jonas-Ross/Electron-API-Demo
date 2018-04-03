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
          message: "Dialogs look native to the platform that the application is running on!",
          buttons: ["Great!"]
        })
      },
      showNativeErrorDialog() {
        const {dialog} = require('electron').remote
        dialog.showErrorBox(
          "This is an error",
          "This is what an error looks like! Here you can specify the exact message you want your user to see."
        )
      },
      handleCrash() {
        const {BrowserWindow, dialog} = require('electron').remote
        const path = require('path')

        const processCrashBtn = document.getElementById('process-crash')

        processCrashBtn.addEventListener('click', (event) => {
          const crashWinPath = path.join('file://', __dirname, '../../sections/windows/process-crash.html')
          let win = new BrowserWindow({ width: 400, height: 320 })

          win.webContents.on('crashed', () => {
            const options = {
              type: 'info',
              title: 'Renderer Process Crashed',
              message: 'This process has crashed.',
              buttons: ['Reload', 'Close']
            }

            dialog.showMessageBox(options, (index) => {
              if (index === 0) win.reload()
              else win.close()
            })
          })

          win.on('close', () => { win = null })
          win.loadURL(crashWinPath)
          win.show()
        })
      }
    },
  };
</script>

<style scoped>

</style>