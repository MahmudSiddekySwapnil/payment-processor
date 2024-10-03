<template>
  <div class="payment-options-container">
    <!-- Single Card that holds all payment options -->
    <div class="payment-card">

      <!-- Card Header with logo -->
      <div class="card-header">
        <img class="site-logo" src="/images/customersite_logo.png" alt="Customer Site Logo" />
      </div>

      <!-- Main Payment Options (MFS, Internet Banking, Card Payments) -->
      <div class="main-buttons">
        <button
            v-for="option in mainPaymentOptions"
            :key="option.id"
            :class="['payment-button', { active: selectedMainOption === option.id }]"
            @click="selectMainOption(option.id)"
        >
          {{ option.name }}
        </button>
      </div>

      <!-- Selected Option Details -->
      <div v-if="selectedMainOption" class="payment-methods-container">
        <h3>Available {{ selectedOptionName }} Methods</h3>
        <div class="sub-buttons">
          <button
              v-for="method in selectedMethods"
              :key="method.id"
              class="method-button"
              @click="selectMethod(method.id)"
          >
            <img
                :src="method.logo"
                :alt="method.name"
                :class="{ 'hover-effect': method.hoverImage }"
                @mouseover="method.logo = method.hoverImage"
                @mouseleave="method.logo = method.defaultLogo"
            />
            <p>{{ method.name }}</p>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mainPaymentOptions: [
        { id: 'card_payments', name: 'Cards' },
        { id: 'mfs', name: 'MFS' },
        { id: 'internet_banking', name: 'I-Banking' },
      ],
      selectedMainOption: 'card_payments', // Default selected option
      paymentMethods: {
        mfs: [
          { id: 'bkash', defaultLogo: '/images/bkash_h.png', hoverImage: '/images/bkash.png', logo: '/images/bkash_h.png' },
          { id: 'nagad', defaultLogo: '/images/nagad_h.png', hoverImage: '/images/nagad.png', logo: '/images/nagad_h.png' },
          { id: 'rocket', defaultLogo: '/images/roket_h.png', hoverImage: '/images/roket.png', logo: '/images/roket_h.png' },
          { id: 'bkash', defaultLogo: '/images/bkash_h.png', hoverImage: '/images/bkash.png', logo: '/images/bkash_h.png' },
          { id: 'nagad', defaultLogo: '/images/nagad_h.png', hoverImage: '/images/nagad.png', logo: '/images/nagad_h.png' },
          { id: 'rocket', defaultLogo: '/images/roket_h.png', hoverImage: '/images/roket.png', logo: '/images/roket_h.png' },
          { id: 'bkash', defaultLogo: '/images/bkash_h.png', hoverImage: '/images/bkash.png', logo: '/images/bkash_h.png' },
          { id: 'nagad', defaultLogo: '/images/nagad_h.png', hoverImage: '/images/nagad.png', logo: '/images/nagad_h.png' },
          { id: 'rocket', defaultLogo: '/images/roket_h.png', hoverImage: '/images/roket.png', logo: '/images/roket_h.png' },
        ],
        internet_banking: [
          { id: 'dbbl', name: 'DBBL Nexus', logo: '/images/dbbl.png' },
          { id: 'brac', name: 'BRAC Bank', logo: '/images/brac.png' },
          { id: 'ebl', name: 'EBL', logo: '/images/ebl.png' },
        ],
        card_payments: [
          { id: 'visa', name: 'Visa', logo: '/images/visa.png' },
          { id: 'mastercard', name: 'MasterCard', logo: '/images/mastercard.png' },
          { id: 'amex', name: 'American Express', logo: '/images/amex.png' },
        ],
      },
    };
  },
  computed: {
    selectedOptionName() {
      const option = this.mainPaymentOptions.find((opt) => opt.id === this.selectedMainOption);
      return option ? option.name : '';
    },
    selectedMethods() {
      return this.paymentMethods[this.selectedMainOption] || [];
    },
  },
  methods: {
    selectMainOption(optionId) {
      this.selectedMainOption = optionId;
    },
    selectMethod(methodId) {
      console.log(`Selected payment method: ${methodId}`);
    },
  },
};
</script>

<style scoped>
.payment-options-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f5f5f5;
}

.payment-card {
  background-color: white;
  border: 2px solid #ccc;
  border-radius: 10px;
  padding: 40px;
  text-align: center;
  width: 600px;
  box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.2);
}

.card-header {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.site-logo {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid #ccc;
  margin-top: -130px;
  background-color: #ecf2f5;
}

.main-buttons {
  margin-top: 20px;
}

.payment-button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 30px;
  border-radius: 5px;
  border: 2px solid #007bff;
  background-color: #007bff;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
  position: relative;
}

.payment-button:hover {
  background-color: #0056b3;
}

.payment-button.active::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  right: 0;
  height: 3px;
  background-color: #121e2a;
  border-radius: 5px;
}


.payment-methods-container {
  margin-top: 20px;
}

.sub-buttons {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px;
  max-height: 600px; /* Max height of the container */
  overflow-y: auto;  /* Enable vertical scrolling */
  margin-top: 15px;
}

.method-button {
  border: none;
  background-color: transparent;
  cursor: pointer;
  text-align: center;
  padding: 10px;
}

.method-button:hover {
  background-color: #f0f0f0;
  border-radius: 10px;
  transition: background-color 0.3s;
}

.method-button img {
  max-width: 400px; /* Adjust to keep images within card */
  margin-bottom: 5px;
}

.method-button p {
  font-size: 14px;
  margin: 0;
}
</style>
