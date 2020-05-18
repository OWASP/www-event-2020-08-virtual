<style>
[v-cloak] {display: none}

.event h1, .event h2, .event h3 {
  margin-left: 0;
}

.event-information {
  margin-bottom: 40px;
}

.ticket-option {
  margin-bottom: 32px;
  padding-bottom: 32px;
  display: flex;
  border-bottom: 1px solid #d3d3d3;
}

.ticket-option:last-child {
  border-bottom: 0;
  margin-bottom: 0;
  padding-bottom: 0;
}

.ticket-buy-button {
  width: 280px;
  text-align: right;
}

.ticket-button {
  border: 1px solid #d3d3d3;
  font-size: 85%;
  padding: 10px;
  background-color: #ffffff;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
  cursor: pointer;
  display: inline-block;
  text-align: center;
}

.ticket-button:hover {
  background-color: #000000 !important;
  color: #ffffff;
}

.ticket-button.selected {
  background-color: {{ include.primary_color | default: "#ff0000" }};
  color: #ffffff;
}

.ticket-button .product-notice {
  font-size: 50%;
}

.ticket-option-information {
  flex: 1;
}

.ticket-option-title {
  font-weight: bold;
  font-size: 105%;
  margin-bottom: 6px;
  cursor: pointer;
}

.ticket-option-description {
  font-size: 85%;
}

.ticket-listing {
  padding-bottom: 40px;
  margin-bottom: 50px;
  border-bottom: 1px solid #000000;
}

.registration-container {
  margin-top: 40px;
  max-width: 70%;
}

.pad-field {
  margin-bottom: 10px;
}

.extra-pad {
  margin-bottom: 25px;
}

.registration-form {
  max-width: 70%;
}

.registration-form input {
  width: 100%;
  border: 1px solid #000000;
  padding: 8px;
  font: inherit;
}

.checkbox-container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.checkbox-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkbox-container .checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
}

.checkbox-container:hover input ~ .checkmark {
  background-color: #ccc;
}

.checkbox-container input:checked ~ .checkmark {
  background-color: {{ include.primary_color | default: "#ff0000" }};
}

.checkbox-container .checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-container input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

.multiselect__option--highlight {
  background: {{ include.primary_color | default: "#ff0000" }} !important;
}

.multiselect__tags {
  border-radius: 0px !important;
  border: 1px solid #000000 !important;
}

.multiselect__tag, .multiselect__tag:hover, .multiselect__tag-icon:hover, .multiselect__tag-icon:after {
  background: {{ include.primary_color | default: "#ff0000" }} !important;
  color: #ffffff !important;
}

.error-text {
  color: #ff0000;
  font-size: 75%;
  margin-top: 4px !important;
}

.event ul {
  padding-inline-start: 0;
}

.button-discount-code-container {
  display: flex;
  margin-bottom: 40px;
}

.purchase-button {
  background-color: {{ include.primary_color | default: "#ff0000" }};
  color: #ffffff;
}

.purchase-button:hover {
  background-color: #8B0000;
}

.help-text {
  font-size: 70%;
}

@media (max-width: 768px) {
  .registration-container, registration-form {
    max-width: 100%;
  }
}
</style>

{% raw %}
<div id="registration-app" class="registration-container" v-cloak>
  <div class="ticket-listing">
    <h2 style="margin-bottom: 30px;">Select your Tickets</h2>
    <div class="error-text" v-if="errors.product">{{ errors.product[0] }}</div>
    <div class="ticket-option" v-for="product in productListing">
        <div v-bind:id="product.sku" class="ticket-option-information">
          <section v-bind:id="product.sku"></section>
          <div class="ticket-option-title" v-on:click="toggleProduct(product.sku)">{{ product.name }}</div>
          <div class="ticket-option-description" v-html="product.description"></div>
        </div>
        <div class="ticket-buy-button">
          <div class="cta-button grey" v-on:click="toggleProduct(product.sku)" v-bind:class="{ selected: selectedProducts.includes(product.sku) }">
            <div class="product-price">{{ product.price }}</div>
          </div>
        </div>
    </div>
  </div>

  <div class="registration-form">
    <h2 style="margin-bottom: 30px;">Attendee Information</h2>
    <form v-on:submit.prevent="handleSubmit">
      <div class="pad-field">
        <input type="text" v-model="email" aria-label="Email Address"
        placeholder="Email Address (required)" />
        <div class="error-text" v-if="errors.email">{{ errors.email[0] }}</div>
      </div>
      <div class="extra-pad">
        <input type="text" v-model="email_confirm" aria-label="Confirm Email Address"
        placeholder="Confirm Email Address (required)" />
        <div class="error-text" v-if="errors.email_confirm">{{ errors.email_confirm[0] }}</div>
      </div>
      <div class="pad-field">
        <input type="text" v-model="company" aria-label="Company Name"
        placeholder="Company Name" />
        <div class="error-text" v-if="errors.company">{{ errors.company[0] }}</div>
      </div>
      <div class="extra-pad">
        <input type="text" v-model="title" aria-label="Title"
        placeholder="Title" />
        <div class="error-text" v-if="errors.title">{{ errors.title[0] }}</div>
      </div>
      <div class="extra-pad">
        <input type="text" v-model="name" aria-label="Full Name"
        placeholder="Full Name (required)" />
        <div class="error-text" v-if="errors.name">{{ errors.name[0] }}</div>
      </div>
      <div class="extra-pad" style="display: flex">
        <div style="width: 50%; padding-right: 10px;">
          <multi-select v-bind:options="countries" v-model="country" v-bind:searchable="false" v-bind:show-labels="false" placeholder="Country (required)"></multi-select>
        <div class="error-text" v-if="errors.country">{{ errors.country[0] }}</div>
        </div>
        <div style="width: 50%; padding-left: 10px;">
          <input type="text" v-model="city" aria-label="City"
          placeholder="City (required)" />
          <div class="error-text" v-if="errors.city">{{ errors.city[0] }}</div>
        </div>
      </div>
      <div class="extra-pad">
        <multi-select v-bind:options="experienceOptions" v-model="experience" v-bind:searchable="false" v-bind:show-labels="false" placeholder="Select your experience level (required)"></multi-select>
        <div class="error-text" v-if="errors.experience">{{ errors.experience[0] }}</div>
      </div>
      <div class="extra-pad">
        <multi-select v-bind:options="personaOptions" v-model="persona" v-bind:searchable="false" v-bind:show-labels="false" placeholder="Select your persona (required)"></multi-select>
        <div class="error-text" v-if="errors.persona">{{ errors.persona[0] }}</div>
      </div>
      <div class="extra-pad" v-if="showDietaryRestrictions">
        <multi-select v-bind:options="dietaryRestrictionOptions" v-model="dietary_restrictions" v-bind:searchable="false" v-bind:multiple="true" v-bind:show-labels="false" placeholder="Select your dietary restrictions (if any)"></multi-select>
        <div class="error-text" v-if="errors.dietary_restrictions">{{ errors.dietary_restrictions[0] }}</div>
      </div>
      <div class="extra-pad">
        <label class="checkbox-container">Agree to Terms of Purchase & Attendance <sup><strong>*</strong></sup>
          <input type="checkbox" v-model="terms_of_purchase">
          <span class="checkmark"></span>
        </label>
        <div class="error-text" v-if="errors.terms_of_purchase">{{ errors.terms_of_purchase[0] }}</div>
        <label class="checkbox-container">Join the OWASP Mailing List
          <input type="checkbox" v-model="mailing_list">
          <span class="checkmark"></span>
        </label>
      </div>
      <div class="button-discount-code-container">
        <div style="margin-right: 80px; width: 40%;">
          <div v-if="loading" style="display: flex;">
	    <div style="margin-right: 10px; align-self: center;">
	      <i class="fa-2x fas fa-spinner fa-spin"></i>
	    </div>
            <div style="font-size: 14px; align-self: center;">Preparing your purchase...</div>
          </div>
          <div v-else>
            <button class="cta-button purchase-button" type="submit">Purchase Ticket</button>
          </div>
        </div>
        <div style="flex: 1;">
          <input type="text" class="discount_code" v-model="discount_code" aria-label="Discount Code" placeholder="Discount Code (if applicable)" />
          <div class="error-text" v-if="errors.discount_code">{{ errors.discount_code[0] }}</div>
          <div class="help-text">Note discounts will be applied at checkout</div>
        </div>
      </div>
      <p class="legal-text">* Registrations are accepted on a full-payment, first-come, first-served basis only. Registration fees are non-refundable and non-transferable. For training classes, your email address may be shared with the Trainer for any session prep and tools. Any recording of training sessions is STRICTLY PROHIBITED. By purchasing a registration you automatically agree to comply with the <a href="https://owasp.org/www-policy/operational/conferences-events" target="_blank">OWASP Conference and Event Attendee Policy</a> and consent to receive emails containing information regarding this specific event and any training courses for which you registered.Additionally you can elect to receive marketing emails from us by selecting "Join the OWASP Marketing Mail List." Marketing mails include information and special offers for upcoming conferences, meetings, and other opportunities offered to you. You can revoke your consent to receive Marketing Mail List emails at any time by using the Unsubscribe link found at the bottom of these emails.</p>
      <p class="legal-text">As we all struggle with our collective "new normal" from the global COVID-19 pandemic, the OWASP Foundation is offering a limited number of discounted tickets to our Virtual AppSec Days.  Please <a href = "https://owasp.wufoo.com/forms/virtual-appsec-days-scholarship-application/">Apply Here</a></p>
    </form>
  </div>
</div>
{% endraw %}

<script src="https://unpkg.com/vue"></script>
<script src="https://js.stripe.com/v3"></script>
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.15/lodash.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.13.0/js/solid.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue-scrollto"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.24.0/moment.min.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script src="https://unpkg.com/vue-multiselect@2.1.0"></script>
<link rel="stylesheet" href="https://unpkg.com/vue-multiselect@2.1.0/dist/vue-multiselect.min.css">
<script>
var stripe = Stripe('{{ include.stripe_key | default: "pk_live_mw0B2kiXQTFkD44liAEI03oT00S5AGfSV3" }}');
window.addEventListener('load', function () {
  const app = new Vue({
    data: {
      selectedProducts: [],
      company: null,
      email: null,
      email_confirm: null,
      discount_code: null,
      name: null,
      title: null,
      dietary_restrictions: null,
      experience: null,
      persona: null,
      country: null,
      city: null,
      terms_of_purchase: false,
      mailing_list: false,
      products: {{ site.data.products | jsonify }},
      countries: {{ site.data.countries | jsonify }},
      errors: {},
      loading: false,
      experienceOptions: [
        'Beginner',
        'Intermediate',
        'Advanced'
      ],
      personaOptions: [
        'Defender',
        'Builder',
        'Breaker',
	'Other'
      ],
      dietaryRestrictionOptions: [
        'Gluten-Free',
        'Halal',
        'Kosher',
        'Nut Allergy',
        'Shellfish Allergy',
        'Vegan',
        'Vegetarian'
      ],
      showDietaryRestrictions: {{ include.show_dietary_restrictions | default: true }}
    },
    components: {
      MultiSelect: window.VueMultiselect.default
    },
    created: function(){
      const queryParams = new URLSearchParams(window.location.search);
      if (queryParams.has('id')) {
        prod_sku = queryParams.get('id');
        this.toggleProduct(prod_sku);
        this.$nextTick(function () {
          VueScrollTo.scrollTo('#' + prod_sku);
        })
      }
    },
    computed: {
      productListing: function () {
        let vm = this;
        let products = [];
        let productListing = _.orderBy(this.products.products, function (product) {
          return product.metadata.display_order;
        });
        _.each(productListing, function (product) {
          let shouldDisplay = true;
          if (product.metadata.display_start || product.metadata.display_end) {
            if (product.metadata.display_start) {
              let display_start = moment(product.metadata.display_start)
              if (moment() < display_start) {
                shouldDisplay = false;
              }
            }
            if (product.metadata.display_end) {
              let display_end = moment(product.metadata.display_end)
              if (moment() > display_end) {
                shouldDisplay = false;
              }
            }
          }
          if (shouldDisplay) {
            products.push({
              sku: product.id,
              name: product.name,
              amount: product.amount,
              price: vm.formatPrice(product.amount),
              description: product.metadata.description
            });
          }
        });
        return products;
      }
    },
    watch: {
      selectedProduct: function (newValue) {
        this.$nextTick(function () {
          VueScrollTo.scrollTo('#registration-information');
        })
      }
    },
    methods: {
      formatPrice: function (amount) {
        const formatter = new Intl.NumberFormat('en-US', {
          style: 'currency',
          currency: this.products.currency,
          minimumFractionDigits: 2
        });
        return formatter.format(amount / 100);
      },
      selectProduct: function (sku) {
        this.selectedProduct = sku;
      },
      handleSubmit: function () {
        let vm = this;
        vm.loading = true;
        vm.validateForm();
        if (Object.keys(vm.errors).length > 0) {
          vm.loading = false;
          vm.$nextTick(function () {
            VueScrollTo.scrollTo('.error-text');
          })
        } else {
          const postData = {
            name: vm.name,
            company: vm.company,
            email: vm.email,
            title: vm.title,
            dietary_restrictions: vm.dietary_restrictions,
            experience: vm.experience,
            persona: vm.persona,
            country: vm.country,
            city: vm.city,
            sku: vm.selectedProducts,
            discount_code: vm.discount_code,
            mailing_list: vm.mailing_list
          }
          axios.post('{{ include.checkout_url | default: "https://owaspadmin.azurewebsites.net/api/EventsCheckout?code=qIyazIloMxpvGtTkSI0cXNoDEwzNIcFe9xp7bGm54t0lakuBEKJ73Q==" }}', postData).then(function (response) {
            if (response.data.data.response_type && response.data.data.response_type === 'redirect') {
              window.location.href = response.data.data.redirect_url
            } else {
              stripe.redirectToCheckout({
                sessionId: response.data.data.session_id
              }).then(function (result) {
                console.log(result.error.message)
              }); 
            }
	  }).catch(function (error) {
	    vm.errors = error.response.data.errors
	    vm.loading = false
	    vm.$nextTick(function () {
	      VueScrollTo.scrollTo('.error-text');
	    })
	  });
	}
      },
      validateForm: function () {
        let errors = {};

        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.email)) {
          errors.email = ['Please enter a valid email address'];
        } else {
          if (this.email !== this.email_confirm) {
            errors.email_confirm = ['These email addresses do not match'];
          }
        }

        if (!this.name) {
          errors.name = ['Name is required'];
        }

        if (!this.country) {
          errors.country = ['Country is required'];
        }

        if (!this.city) {
          errors.city = ['City is required'];
        }

        if (!this.experience) {
          errors.experience = ['Experience level is required'];
        }

        if (!this.persona) {
          errors.persona = ['Persona is required'];
        }

        if (!this.selectedProducts.length) {
          errors.product = ['Please select a ticket option below']
        }
        
        if (!this.terms_of_purchase) {
          errors.terms_of_purchase = ['You must agree to the terms of puchase']
        }

        this.errors = errors;
      },
      toggleProduct: function (sku) {
        if (this.selectedProducts.includes(sku)) {
          const existingIndex = _.findIndex(this.selectedProducts, function (product) {
            return product === sku
          })
          if (existingIndex !== -1) {
            this.selectedProducts.splice(existingIndex, 1)
          }
        } else {
          this.selectedProducts.push(sku)
        }
      }
    }
  }).$mount('#registration-app')
})
</script>
