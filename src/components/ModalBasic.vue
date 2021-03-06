<template>
  <modal
    :name="name"
    :classes="'s-modal-wrapper'"
    :maxWidth="width"
    :minWidth="minWidth"
    height="auto"
    :adaptive="true"
    v-on="$listeners"
    :clickToClose="clickToClose"
  >
    <div class="s-modal-container">
      <div class="s-modal-body">
        <div class="s-normal-upper">
          <h1 v-if="!!title" class="s-modal-title">{{ title }}</h1>
          <h2 v-if="!!subTitle" class="s-modal-sub-title">{{ subTitle }}</h2>
          <p v-if="!!text" class="s-modal-text">{{ text }}</p>
          <slot></slot>
        </div>
      </div>
      <div
        class="s-modal-footer"
        v-if="!hideActionButtons && hideActionButtons !== ''"
      >
        <div class="s-modal-footer-inner s-button-container">
          <Button
            :variation="'default'"
            :title="'Close'"
            :size="'fixed-width'"
            @click="$modal.hide(name)"
          ></Button>
          <Button
            :variation="'action'"
            :title="confirmButtonText"
            :size="'fixed-width'"
            @click="$emit('confirm')"
          ></Button>
        </div>
      </div>
    </div>
  </modal>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Button from "./../components/Button.vue";

@Component({
  components: {
    Button
  }
})
export default class ModalBasic extends Vue {
  @Prop()
  name!: string;

  @Prop({ default: 600 })
  width!: number;

  @Prop({ default: 600 })
  minWidth!: number;

  @Prop()
  title!: string;

  @Prop()
  subTitle!: string;

  @Prop()
  text!: string;

  @Prop()
  hideActionButtons!: string;

  @Prop({ default: "Confirm" })
  confirmButtonText!: string;

  @Prop({ default: true })
  clickToClose!: boolean;
}
</script>

<style lang="less" scoped>
@import (reference) "./../styles/Imports";
@import "./../styles/components/Modals";

.s-modal-body {
  border-radius: 8px 8px 0 0;
}

.s-modal-footer {
  background: @light-2;
  .radius-bottom(2);
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.s-modal-footer-inner {
  .padding-v-sides(2);
  .padding-h-sides(3);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
}

.night,
.night-theme {
  .s-modal-body {
    background: @night-shadow;
  }

  .s-modal-footer {
    background: @dark-2;
  }
}
</style>
