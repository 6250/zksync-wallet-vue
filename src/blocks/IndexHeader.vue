<template>
  <i-layout-header class="indexHeader" :class="{ opened: opened }">
    <div class="mobileIndexHeader">
      <i-container class="mobileOnly">
        <i-row class="_display-flex _justify-content-between _flex-nowrap">
          <i-column>
            <transition name="fade">
              <block-logo :is-zk-sync-logo="true" />
            </transition>
          </i-column>
          <i-column class="_padding-right-0">
            <div class="hamContainer">
              <svg id="ham" viewBox="0 0 100 100" width="80" @click="opened = !opened">
                <path
                  class="line top"
                  d="m 30,33 h 40 c 0,0 9.044436,-0.654587 9.044436,-8.508902 0,-7.854315 -8.024349,-11.958003 -14.89975,-10.85914 -6.875401,1.098863 -13.637059,4.171617 -13.637059,16.368042 v 40"
                />
                <path class="line middle" d="m 30,50 h 40" />
                <path
                  class="line bottom"
                  d="m 30,67 h 40 c 12.796276,0 15.357889,-11.717785 15.357889,-26.851538 0,-15.133752 -4.786586,-27.274118 -16.667516,-27.274118 -11.88093,0 -18.499247,6.994427 -18.435284,17.125656 l 0.252538,40"
                />
              </svg>
            </div>
          </i-column>
        </i-row>
      </i-container>
    </div>
    <div class="mainIndexHeader">
      <i-container>
        <i-row>
          <i-column :xs="12" :md="4" class="_padding-left-0 desktopOnly">
            <block-logo :is-zk-sync-logo="true" />
          </i-column>
          <i-column :xs="12" :md="4" class="_padding-y-0">
            <div class="linksContainer">
              <a href="https://zksync.io/faq/" target="_blank" class="linkItem">FAQ</a>
              <a href="https://zksync.io/dev/" target="_blank" class="linkItem">Docs</a>
              <i-dropdown
                class="_background-transparent _border-none likeLinkItem"
                :class="{ opened: dropdownOpened }"
                size="sm"
                variation="dark"
                placement="bottom"
                trigger="click"
              >
                <a class="dropDownHandler linkItem _position-top-0" @click.capture="dropdownOpened = !dropdownOpened">
                  zkTools <v-icon class="fal" :name="dropdownOpened ? 'ri-arrow-up-s-line' : 'ri-arrow-down-s-line'" />
                </a>
                <i-dropdown-menu v-model="dropdownOpened">
                  <i-dropdown-item v-for="(item, index) in dropdownOptions" :key="index" :href="item.link" target="_blank">{{ item.name }}</i-dropdown-item>
                </i-dropdown-menu>
              </i-dropdown>
              <a href="https://matter-labs.io/#jobs" target="_blank" class="linkItem">We're hiring</a>
            </div>
          </i-column>
          <i-column :xs="12" :md="4" class="_margin-left-auto _padding-right-0 _justify-content-end desktopOnly">
            <block-social-block />
          </i-column>
        </i-row>
      </i-container>
    </div>
  </i-layout-header>
</template>

<script lang="ts">
import Vue from "vue";
import { ZkConfig } from "matter-dapp-module/types";

interface DropdownOption {
  name: string;
  link: string;
}

export default Vue.extend({
  name: "IndexHeader",
  data() {
    const config: ZkConfig = this.$store.getters["zk-onboard/config"];
    return {
      opened: false,
      dropdownOpened: false,
      dropdownOptions: <DropdownOption[]>[
        {
          name: "zkScan",
          link: config.zkSyncNetwork.explorer,
        },
        {
          name: "zkLink",
          link: config.zkSyncNetwork.tools.link,
        },
        {
          name: "Alternative Withdrawal",
          link: config.zkSyncNetwork.tools.withdrawal,
        },
        {
          name: "zkMint",
          link: config.zkSyncNetwork.tools.mint,
        },
      ],
    };
  },
});
</script>
