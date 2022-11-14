<template>
  <div
    class="card"
    :style="{ width: `${width}px` }"
    v-click-outside="clickOutside"
    ref="cardRef"
  >
    <div
      :class="['card-image']"
      @click="!isClickDisable && $emit('onCardClick')"
    >
      <img
        :class="[
          'card-thumbnail',
          imgClass,
          { disableCard: isClickDisable },
          { blockIcon: showBlockIcon && isClickDisable }
        ]"
        :src="image"
      />
      <img
        v-if="showPlayIcon && !isClickDisable"
        :class="['card-icon', { disableCard: isClickDisable }]"
        src="https://dp3k82tjmkfj0.cloudfront.net/assets/library/play_icon.svg"
      />
    </div>
    <div class="card-content">
      <div class="card-content-details">
        <ToolTip :toolTipMessage="title" alignment="center" class="tooltip">
          <GoldcastText
            :noOfLineEllipsis="3"
            textAlign="start"
            :fontWeight="400"
            class="card-content-title"
          >
            {{ title }}
          </GoldcastText>
        </ToolTip>
        <div class="card-content-subtile">
          <GoldcastText
            color="rgba(28, 30, 31, 0.4)"
            :font-size="11"
            textAlign="start"
            class="subTitle"
          >
            {{ subTitle }}
          </GoldcastText>
          <v-btn
            v-if="showCtaButton"
            xSmall
            outlined
            color="primary"
            @click="handleStatusAction"
            >{{ ctaButtonText }}
          </v-btn>
          <InfoTooltip v-if="tooltipText" :iconColor="isError ? 'red' : 'grey'">
            <template #contentOne>
              <GoldcastText :fontSize="12" color="rgba(28, 30, 31, 0.6)">
                {{ tooltipText }}
              </GoldcastText>
            </template>
          </InfoTooltip>
        </div>
      </div>
      <div class="card-content-action">
        <img
          src="https://dp3k82tjmkfj0.cloudfront.net/assets/event-list/menu-icon.svg"
          @click="handleAction"
        />
        <div
          :class="`card-content-action-item ${dropdownOpenDirectionClass}`"
          v-if="isDropDownOpen"
        >
          <MenuItems :options="dropdownCta" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import InfoTooltip from '../components/common/InfoTooltip';
import GoldcastText from '../components/core/GoldcastText.vue';
import MenuItems from './MenuItems.vue';

export default {
  name: 'Card',
  components: { GoldcastText, MenuItems, InfoTooltip },
  props: {
    image: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    subTitle: {
      type: String,
      default: null
    },
    tooltipText: {
      type: String,
      default: null
    },
    showCtaButton: {
      type: Boolean,
      default: false
    },
    ctaButtonText: {
      type: String,
      default: 'Process'
    },
    isError: {
      type: Boolean,
      default: false
    },
    dropdownCta: {
      type: Array,
      required: true
    },
    width: {
      type: Number,
      required: true
    },
    isClickDisable: {
      type: Boolean,
      default: true
    },
    imgClass: {
      type: String,
      default: ''
    },
    showPlayIcon: {
      type: Boolean,
      default: false
    },
    showBlockIcon: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isDropDownOpen: false,
      dropdownOpenDirectionClass: ''
    };
  },
  methods: {
    handleAction() {
      const box = this.$refs.cardRef;
      const positionData = box.getBoundingClientRect();
      const availableHeight = window.innerHeight - positionData.bottom;
      const availableWidth = window.innerWidth - positionData.right;
      this.dropdownOpenDirectionClass =
        availableHeight > 300 ? 'open-bottom' : 'open-up';
      this.dropdownOpenDirectionClass +=
        availableWidth < this.width ? ' open-left' : '';
      this.isDropDownOpen = !this.isDropDownOpen;
    },
    handleStatusAction() {
      this.$emit('onClickCta');
    },
    clickOutside() {
      this.isDropDownOpen = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.card {
  background-color: white;
  padding: 8px;
  border-radius: 8px;
  &-image {
    position: relative;
  }
  &-icon {
    cursor: pointer;
    position: absolute;
    top: 37%;
    left: 43%;
  }
  &-thumbnail {
    width: 100%;
    height: 130px;
    border-radius: 8px;
    cursor: pointer;
  }

  &-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    &-details {
      flex: 4;
    }
    &-title {
      display: block !important;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      opacity: 0.75;
    }
    &-subtile {
      display: flex;
      align-items: center;
      margin-top: 2px;
    }
    &-action {
      position: relative;
      flex: 1;
      justify-content: flex-end;
      display: flex;

      & > img {
        padding: 5px 10px;
        cursor: pointer;
        &:hover {
          background-color: #e3e7f0;
          border-radius: 50%;
        }
      }
      &-item {
        z-index: 1;
        position: absolute;
      }
    }
  }
  .open-bottom {
    left: 25px;
    top: 20px;
  }
  .open-up {
    left: unset;
    bottom: 20px;
  }
  .open-left {
    left: unset;
  }
  .tooltip {
    display: grid;
  }
  .disableCard {
    cursor: default;
  }
  .blockIcon {
    cursor: not-allowed;
  }
  .imageSection {
    object-fit: contain;
  }
  .subTitle {
    margin-bottom: 5px;
  }
}
</style>
