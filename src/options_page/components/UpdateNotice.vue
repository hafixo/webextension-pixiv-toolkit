<template>
  <v-dialog
    v-model="show"
    width="50%"
    :scrollable="true"
  >
    <v-card>
      <v-card-title class="headline grey lighten-2" primary-title>Change Log</v-card-title>

      <v-card-text>
        <change-log></change-log>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn flat @click="show = false">{{ tl('_close') }}</v-btn>
        <v-btn color="primary" flat @click="closeNotice">{{ tl('_do_not_show_again') }}</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import SuperMixin from "@/mixins/SuperMixin";
import ChangeLog from '@/options_page/components/ChangeLog'

export default {
  mixins: [
    SuperMixin
  ],

  components: {
    'change-log': ChangeLog
  },

  data() {
    return {
      show: false
    }
  },

  mounted() {
    if (!this.browserItems.importantNoticeDisplayed) {
      this.show = true;
    }
  },

  methods: {
    closeNotice() {
      browser.storage.local.set({ importantNoticeDisplayed: true });

      this.show = false;
    }
  }
};
</script>
