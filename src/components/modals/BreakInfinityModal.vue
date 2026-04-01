<script>
import ModalWrapperChoice from "@/components/modals/ModalWrapperChoice";

export default {
  name: "BreakInfinityModal",
  components: {
    ModalWrapperChoice
  },
  computed: {
    message() {
      const infinity = formatPostBreak(Number.MAX_VALUE, 2);
      return `Fixing Infinity will prevent you to gain antimatter past ${infinity}${PlayerProgress.eternityUnlocked()
        ? "." : `, and allow you to read numbers below ${infinity}.`}
        Dimensions and Tickspeed Upgrades will scale in cost faster below -${infinity} antimatter.
        You will gain additional Infinity Points on Big Crunch based on antimatter decayed over ${infinity}.\
        ${EternityMilestone.keepAutobuyers.isReached ? "" : `\nIt will also unlock Fix Infinity Upgrades and max\
        all Normal Challenge Autobuyers.`}`.split("\n");
    },
  },
  methods: {
    handleYesClick() {
      breakInfinity();
    }
  },
};
</script>

<template>
  <ModalWrapperChoice
    :show-cancel="false"
    @confirm="handleYesClick"
  >
    <template #header>
      You are Fixing Infinity
    </template>
    <div class="c-modal-message__text">
      <span
        v-for="(line, index) in message"
        :key="index"
      >
        {{ line }} <br>
      </span>
    </div>
    <template #confirm-text>
      Fix
    </template>
  </ModalWrapperChoice>
</template>
