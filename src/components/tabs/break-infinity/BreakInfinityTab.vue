<script>
import BreakInfinityButton from "./BreakInfinityButton";
import InfinityUpgradeButton from "@/components/InfinityUpgradeButton";

export default {
  name: "BreakInfinityTab",
  components: {
    BreakInfinityButton,
    InfinityUpgradeButton
  },
  data() {
    return {
      isUnlocked: false
    };
  },
  computed: {
    grid() {
      return [
        [
          BreakInfinityUpgrade.ipGen,
          BreakInfinityUpgrade.ipGen,
          BreakInfinityUpgrade.ipGen,
          BreakInfinityUpgrade.dimCostMult,
          BreakInfinityUpgrade.tickspeedCostMult,
        ],
        [
          BreakInfinityUpgrade.autobuyerSpeed,
          BreakInfinityUpgrade.autobuyMaxDimboosts,
          BreakInfinityUpgrade.infinitiedGen,
          BreakInfinityUpgrade.infinitiedGen,
          BreakInfinityUpgrade.infinitiedGen,
        ],
        [
          BreakInfinityUpgrade.slowestChallengeMult,
          BreakInfinityUpgrade.achievementMult,
          BreakInfinityUpgrade.infinitiedMult,
          BreakInfinityUpgrade.infinitiedMult,
          BreakInfinityUpgrade.infinitiedMult,
        ],
        [
          BreakInfinityUpgrade.galaxyBoost,
          BreakInfinityUpgrade.currentAMMult,
          BreakInfinityUpgrade.totalAMMult,
          BreakInfinityUpgrade.totalAMMult,
          BreakInfinityUpgrade.totalAMMult,
        ],
      ];
    }
  },
  methods: {
    update() {
      this.isUnlocked = Autobuyer.bigCrunch.hasMaxedInterval;
    },
    btnClassObject(column) {
      return {
        "l-infinity-upgrade-grid__cell": true,
        "o-infinity-upgrade-btn--multiplier": column === 3
      };
    },
    timeDisplayShort(time) {
      return timeDisplayShort(time);
    }
  }
};
</script>

<template>
  <div class="l-break-infinity-tab">
    <div v-if="!isUnlocked">
      Reduce the interval of Automatic Big Crunch Autobuyer to
      {{ format(0.1, 1, 1) }} seconds to unlock Fix Infinity.
    </div>
    <BreakInfinityButton class="l-break-infinity-tab__break-btn" />
    <div
      v-if="isUnlocked"
      class="l-break-infinity-upgrade-grid l-break-infinity-tab__grid"
    >
      <div
        v-for="(column, columnId) in grid"
        :key="columnId"
        class="l-break-infinity-upgrade-grid__row"
      >
        <InfinityUpgradeButton
          v-for="upgrade in column"
          :key="upgrade.id + Math.random()"
          :upgrade="upgrade"
          :class="btnClassObject(columnId)"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
