<script>
import stylesService from "@/shared/styles/styles.service";
import {getFooterInfo} from "@/public/services/footer-data.service";

export default {
  methods: {
    loadFooterInfo(){
      getFooterInfo()
          .then((response)=>{
            this.footerInfo = response;
            console.log(response)
          })
          .catch((error)=>{
            console.log(error)
          })
    },
    getMode(newDarkMode){
      this.isDarkMode = newDarkMode;
      this.currentMode = stylesService.methods.getCurrentMode();
    }
  },
  data() {
    return {
      footerInfo: null,
      isDarkMode: false,
      currentMode: "light"
    };
  },
  created() {
    this.loadFooterInfo();
    this.isDarkMode = stylesService.methods.watchDarkMode(this.getMode);
    this.currentMode = stylesService.methods.getCurrentMode();
  }
}
</script>


<template>
  <pv-toolbar id="footer" class="footer width-full">
    <template #start>
      <div class="flex flex-justify-content flex-col width-full">
        <div class="flex flex-justify-content flex-row">
          <div/>
          <pv-image :src="`/images/logos/${this.currentMode}/logo.png`" alt="Akira" class="footer-logo"/>
          <div/>
          <div class="flex-row">
            <div v-for="(section, index) in footerInfo" :key="index" class="right-padding-2">
              <div><h2>{{ section.title }}</h2></div>
              <div v-for="(item, itemIndex) in section.content"
                   :key="itemIndex"
                   class="left-padding-1 flex flex-row"
              >
                <pv-image v-if="item.img !== ''" :src="`/images/social-networks/${this.currentMode}/${item.img}.svg`" class="footer-icons" />
                <router-link :to="item.to" class="text">
                  {{ item.label }}
                </router-link>
              </div>
            </div>
          </div>
          <div/>
        </div>
        <pv-divider/>
        <div class="flex flex-justify-content flex-row width-full">
          <div class="flex flex-justify-content text width-padding-3">&copy; Akira, Lambders 2022</div>
          <pv-image src="/images/logos/methods.png" alt="Metodos de Pago" class="payment-image width-padding-3"/>
        </div>
      </div>

    </template>
  </pv-toolbar>
</template>


<style>
#footer{
  width: 100%;
  outline: none;
}
.text{

}
</style>