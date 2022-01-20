<template>
  <div>
    <form ref="form" class="form" @submit.prevent="submitForm">
      <div class="form__left-col">
        <h3>представтесь, пожалуйста</h3>

        <div class="form__field-wrapper">
          <label for="lastname">* фамилия</label>
          <input type="text" id="lastname" v-model="lastName" required />
          <span v-if="errorMsg.lastName">{{ errorMsg.lastName }}</span>
        </div>

        <div class="form__field-wrapper">
          <label for="firstname">* имя</label>
          <input type="text" id="firstname" v-model="firstName" required />
          <span v-if="errorMsg.firstName">{{ errorMsg.firstName }}</span>
        </div>

        <div class="form__field-wrapper">
          <label for="organization">организация и должность</label>
          <input type="text" id="organization" v-model="organization" />
          <span v-if="errorMsg.organization">{{ errorMsg.organization }}</span>
        </div>

        <div class="form__radio-wrapper">
          <input type="radio" name="radio" id="radio-1" value="потребитель" />
          <label for="radio-1">потребитель</label>
        </div>

        <div class="form__radio-wrapper">
          <input
            type="radio"
            name="radio"
            id="radio-2"
            value="медицинский работник"
          />
          <label for="radio-2">медицинский работник</label>
        </div>

        <div class="form__radio-wrapper">
          <input type="radio" name="radio" id="radio-3" value="журналист" />
          <label for="radio-3">журналист</label>
        </div>

        <h3>сообщение</h3>

        <div class="form__field-wrapper">
          <label for="msg-theme">тема сообщения</label>
          <input type="text" id="msg-theme" v-model="msgTheme" />
          <span v-if="errorMsg.msgTheme">{{ errorMsg.msgTheme }}</span>
        </div>

        <div class="form__field-wrapper">
          <label for="msg">* сообщение</label>
          <textarea type="text" id="msg" v-model="msg" required />
          <span v-if="errorMsg.msg">{{ errorMsg.msg }}</span>
        </div>
      </div>
      <div class="form__right-col">
        <h3>контактная информация</h3>
        <div class="form__field-wrapper">
          <label for="email">* email</label>
          <input type="email" name="" id="email" required />
        </div>

        <div class="form__field-wrapper">
          <label for="country">страна</label>
          <input type="text" id="country" v-model="country" />
          <span v-if="errorMsg.country">{{ errorMsg.country }}</span>
        </div>

        <div class="form__field-wrapper">
          <label for="city">город</label>
          <input type="text" id="city" v-model="city" />
          <span v-if="errorMsg.city">{{ errorMsg.city }}</span>
        </div>

        <div class="form__field-wrapper">
          <label for="zip">индекс</label>
          <input type="text" id="zip" v-model="zip" />
          <span v-if="errorMsg.zip">{{ errorMsg.zip }}</span>
        </div>

        <div class="form__field-wrapper">
          <label for="address">адрес</label>
          <input type="text" id="address" v-model="address" />
          <span v-if="errorMsg.address">{{ errorMsg.address }}</span>
        </div>

        <div class="form__field-wrapper">
          <label for="phone">* телефон</label>
          <input
            type="text"
            id="phone"
            v-model="phone"
            placeholder="(___) ___-__-__"
            maxlength="10"
            required
          />
          <span v-if="errorMsg.phone">{{ errorMsg.phone }}</span>
        </div>

        <input type="submit" value="отправить" />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lastName: "",
      firstName: "",
      organization: "",
      msgTheme: "",
      msg: "",
      email: "",
      country: "",
      city: "",
      zip: "",
      address: "",
      phone: "",
      errorMsg: {
        lastName: null,
        firstName: null,
        organization: null,
        msgTheme: null,
        msg: null,
        country: null,
        city: null,
        zip: null,
        address: null,
        phone: null,
      },
    };
  },

  methods: {
    validateText(value) {
      if (
        /^[аАбБвВгГдДеЕёЁжЖзЗиИйЙкКлЛмМнНоОпПрРсСтТуУфФхХцЦчЧшШщЩъЪыЫьЬэЭюЮяЯ]+$/.test(
          value
        )
      ) {
        this.errorMsg.lastName = null;
        this.errorMsg.firstName = null;
        this.errorMsg.organization = null;
        this.errorMsg.msgTheme = null;
        this.errorMsg.city = null;
        this.errorMsg.country = null;
        return false;
      } else {
        this.errorMsg.lastName = "Можно использовать только кириллицу";
        this.errorMsg.firstName = "Можно использовать только кириллицу";
        this.errorMsg.organization = "Можно использовать только кириллицу";
        this.errorMsg.msgTheme = "Можно использовать только кириллицу";
        this.errorMsg.city = "Можно использовать только кириллицу";
        this.errorMsg.country = "Можно использовать только кириллицу";
        return true;
      }
    },

    validateZip(value) {
      if (/^[0-9]+$/.test(value)) {
        this.errorMsg["zip"] = null;
        return false;
      } else {
        this.errorMsg["zip"] = "Можно использовать только цифры";
      }
    },

    validateAddress(value) {
      if (
        /^[аАбБвВгГдДеЕёЁжЖзЗиИйЙкКлЛмМнНоОпПрРсСтТуУфФхХцЦчЧшШщЩъЪыЫьЬэЭюЮяЯ0123456789/.,]+$/.test(
          value
        )
      ) {
        this.errorMsg["address"] = null;
        return false;
      } else {
        this.errorMsg["address"] =
          "Можно использовать только кириллицу, цифры, '/', '.', ','";
        return true;
      }
    },

    validatePhone(value) {
      if (/^[0123456789]+$/.test(value)) {
        this.errorMsg["phone"] = null;
        return false;
      } else {
        this.errorMsg["phone"] = "Телефон должен состоять из 10 цифр";
        return true;
      }
    },

    validateMsg(value) {
      if (
        /^[аАбБвВгГдДеЕёЁжЖзЗиИйЙкКлЛмМнНоОпПрРсСтТуУфФхХцЦчЧшШщЩъЪыЫьЬэЭюЮяЯ0123456789]+$/.test(
          value
        )
      ) {
        this.errorMsg["msg"] = null;
        return false;
      } else {
        this.errorMsg["msg"] = "Можно использовать только кириллицу или цифры";
        return true;
      }
    },

    submitForm() {
      if (
        this.validateText(this.lastName) ||
        this.validateText(this.firstName) ||
        this.validateText(this.organization) ||
        this.validateText(this.msgTheme) ||
        this.validateMsg(this.msg) ||
        this.validateText(this.country) ||
        this.validateText(this.city) ||
        this.validateZip(this.zip) ||
        this.validateAddress(this.address) ||
        this.validatePhone(this.phone)
      ) {
        console.log("validation failed");
      } else {
        this.$refs.form.reset();
        alert("отправлено");
      }
    },
  },
};
</script>

<style lang="scss">
.form {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;

  h3 {
    text-transform: uppercase;
    font-weight: 400;
    margin: 1.875rem 0;
  }

  &__left-col,
  &__right-col {
    width: 19.375rem;
    padding: 1rem;
    margin: 3.125rem;
  }

  input[type="text"],
  input[type="email"],
  textarea {
    display: block;
    width: 15.625rem;
    height: 1.875rem;
    margin-bottom: 0.9375rem;
  }

  input[type="radio"] {
    margin-right: 0.3125rem;
  }

  input[type="submit"] {
    display: block;
    width: 15.625rem;
    background: #464646;
    color: white;
    font-size: 1.375rem;
    margin-top: 3.4375rem;
    cursor: pointer;
  }

  label {
    text-transform: uppercase;
    font-size: 0.75rem;
  }

  &__radio-wrapper {
    display: flex;
    margin: 0.625rem 0;
  }

  &__field-wrapper {
    position: relative;

    span {
      position: absolute;
      top: 50px;
      padding-top: 0px;
      margin-top: 0px;
      font-size: 10px;
      color: red;
    }
  }

  @media (max-width: 819px) {
    .form__left-col,
    .form__right-col {
      margin: 0;
    }
  }
}
</style>
