<template>
  <SfAddressPicker
    class="address-picker"
    v-if="addresses && addresses.length > 0"
    :selected="selectedAddressId"
    @change="onSelectAddress"
  >
    <SfAddress
      v-for="address in addresses"
      :key="address._id"
      :name="address._id"
    >
      <span>{{ address.firstName }} {{ address.lastName }}</span>
      <span>{{ address.addressLine1 }}</span>
      <span>{{ address.addressLine2 }}</span>
      <span>{{ address.postalCode }}</span>
      <span>{{ address.city }}, {{ address.state }}</span>
      <span>{{ address.country }}</span>
      <span>{{ address.phone }}</span>
    </SfAddress>
    <SfAddress>
      <span>Other address</span>
    </SfAddress>
  </SfAddressPicker>
</template>

<script>
import { SfAddressPicker } from '@storefront-ui/vue';

export default {
  components: {
    SfAddressPicker
  },
  props: {
    addresses: {
      type: Array,
      default: () => []
    },
    value: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      selectedAddressId: this.value
    };
  },
  methods: {
    onSelectAddress(addressId) {
      this.selectedAddressId = addressId;

      const addressIdToEmit = addressId === '' ? undefined : addressId;
      this.$emit('input', addressIdToEmit);
    }
  },
  watch: {
    value(newValue) {
      this.selectedAddressId = newValue;
    }
  }
};
</script>

<style scoped>
.address-picker {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacer-xs);
  margin-bottom: var(--spacer-xs);
}
</style>
