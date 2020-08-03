<template>
  <div id="app">
    <div class="container">
      <form class="auth-form" novalidate @submit.prevent="submitHandler">
        <h1 class="auth-form__title">Регистрация</h1>
        <div class="form-group" v-show="part===1">
          <div class="form-group__item">
            <label for="surName">
              <span class="form-group__subtitle form-group__subtitle_required">Ваша фамилия</span>
            </label>
            <input class="form-group__textfield" type="text" id="surName"
                   placeholder="Ваше фамилия"
                   v-model.trim="formReg.surName"
                   @blur="$v.formReg.surName.$touch()">
            <small v-if="$v.formReg.surName.$error">
              <template v-if="!$v.formReg.surName.alpha">
                Поле должно содержать только русские буквы
              </template>
              <template v-else>
                Это поле является обязательным
              </template>
            </small>

          </div>
          <div class="form-group__item">
            <label for="firstName">
              <span class="form-group__subtitle form-group__subtitle_required">Ваше имя</span>
            </label>
            <input class="form-group__textfield" type="text" id="firstName"
                   placeholder="Ваше имя"
                   v-model.trim="formReg.name"
                   @blur="$v.formReg.name.$touch()">
            <small v-if="$v.formReg.name.$error">
              <template v-if="!$v.formReg.name.alpha">
                Поле должно содержать только русские буквы
              </template>
              <template v-else>
                Это поле является обязательным
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <label for="thirdName">
              <span class="form-group__subtitle">Ваше отчетсво</span>
            </label>
            <input class="form-group__textfield" type="text" id="thirdName"
                   placeholder="Ваше отчетсво"
                   v-model.trim="formReg.thirdName"
                   @blur="$v.formReg.thirdName.$touch()">
            <small v-if="$v.formReg.thirdName.$error">
              <template v-if="!$v.formReg.thirdName.  alpha">
                Поле должно содержать только русские буквы
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <label for="birthDay">
              <span class="form-group__subtitle form-group__subtitle_required">Дата рождения</span>
            </label>
            <input class="form-group__textfield" type="date" id="birthDay"
                   v-model.trim="formReg.birthDay"
                   @blur="$v.formReg.birthDay.$touch()">
            <small v-if="$v.formReg.birthDay.$error">
              Введите дату Вашего рождения
            </small>
          </div>
          <div class="form-group__item">
            <label for="phoneNumber">
              <span class="form-group__subtitle">Номер телефона</span>
            </label>
            <input class="form-group__textfield" type="tel" id="phoneNumber"
                   placeholder="7xxxxxxxxxx"
                   v-model.trim="formReg.phoneNumber"
                   @blur="$v.formReg.phoneNumber.$touch()">
            <small v-if="$v.formReg.phoneNumber.$error">
              <template v-if="!$v.formReg.phoneNumber.validData">
                Поле должно содержать {{ $v.formReg.phoneNumber.$params.minLength.min }}
                цифр вида: 7xxxxxxxxxx
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <span class="form-group__subtitle">Ваш пол</span>
            <div class="form-group__sex-selection">
              <div class="first-item">
                <input type="radio" name="sex-selection" id="man"
                       value="Мужчина"
                       v-model.trim="formReg.sex">
                <label for="man">Мужчина</label>
              </div>

              <div class="second-item">
                <input type="radio" name="sex-selection" id="woman"
                       value="Женщина"
                       v-model.trim="formReg.sex">
                <label for="woman">Женщина</label>
              </div>
            </div>
          </div>

          <div class="form-group__item">
            <span class="form-group__subtitle form-group__subtitle_required">
                Ваша клиентская группа
            </span>
            <div class="form-group__client-group">
              <select v-model.trim="formReg.clientGroup" required multiple size="3">
                <option>VIP</option>
                <option>Проблемные</option>
                <option>ОМС</option>
              </select>
            </div>
          </div>

          <div class="form-group__item">
            <span class="form-group__subtitle">
                Ваша лечащий врач
            </span>
              <div class="form-group__doctor">
                <select v-model.trim="formReg.doctor">
                  <option selected disabled></option>
                  <option>Иванов</option>
                  <option>Захаров</option>
                  <option>Чернышева</option>
                </select>
              </div>
          </div>

          <div class="form-group__item">
            <label>
              <input type="checkbox" v-model.trim="formReg.mailing"> Не отправлять СМС
            </label>
          </div>
          <div class="form-group__buttons">
            <button type="button" @click="nextPart">Далее</button>
          </div>
        </div>

        <div class="form-group" v-show="part===2">
          <div class="form-group__item">
            <label for="mailIndex">
              <span class="form-group__subtitle">Индекс</span>
            </label>
            <input type="number" id="mailIndex" placeholder="xxxxxx"
                   class="form-group__textfield"
                   v-model.trim="formReg.mailIndex"
                   @blur="$v.formReg.mailIndex.$touch()">
            <small v-if="$v.formReg.mailIndex.$error">
              <template v-if="!$v.formReg.mailIndex.validData">
                Поле должно содержать {{ $v.formReg.mailIndex.$params.minLength.min }}
                цифр формата: xxxxxx
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <label for="country">
              <span class="form-group__subtitle">Страна</span>
            </label>
            <input type="text" id="country" v-model.trim="formReg.country"
                   class="form-group__textfield"
                   @blur="$v.formReg.country.$touch()">
            <small v-if="$v.formReg.country.$error">
              <template v-if="!$v.formReg.country.alpha">
                Поле должно содержать только русские символы
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <label for="region">
              <span class="form-group__subtitle">Область</span>
            </label>
            <input type="text" id="region" v-model.trim="formReg.region"
                   class="form-group__textfield"
                   @blur="$v.formReg.region.$touch()">
            <small v-if="$v.formReg.region.$error">
              <template v-if="!$v.formReg.region.alpha">
                Поле должно содержать только русские символы
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <label for="city">
              <span class="form-group__subtitle form-group__subtitle_required">Город</span>
            </label>
            <input type="text" id="city" v-model.trim="formReg.city"
                   class="form-group__textfield"
                   @blur="$v.formReg.city.$touch()">
            <small v-if="$v.formReg.city.$error">
              <template v-if="!$v.formReg.city.alpha">
                Поле должно содержать только русские символы
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <label for="street">
              <span class="form-group__subtitle">Улица</span>
            </label>
            <input type="text" id="street" v-model.trim="formReg.street"
                   class="form-group__textfield"
                   @blur="$v.formReg.street.$touch()">
            <small v-if="$v.formReg.street.$error">
              <template v-if="!$v.formReg.street.alpha">
                Поле должно содержать только русские символы
              </template>
            </small>
          </div>

          <div class="form-group__item">
            <label for="houseNumber">
              <span class="form-group__subtitle">Дом</span>
            </label>
            <input type="number" id="houseNumber" v-model.trim="formReg.houseNumber"
                   class="form-group__textfield">
          </div>

          <div class="form-group__buttons">
            <button type="button" @click="prevPart">Назад</button>
            <button type="button" @click="nextPart">Далее</button>
          </div>
        </div>

        <div class="form-group" v-show="part===3">
          <div class="form-group__item">
            <span class="form-group__subtitle form-group__subtitle_required">
              Тип документа
            </span>
              <div class="form-group__doctype">
                <select v-model.trim="formReg.docType">
                  <option selected disabled></option>
                  <option>Паспорт</option>
                  <option>Свидетельство о рождении</option>
                  <option>Вод. удостовирение</option>
                </select>
              </div>
          </div>

          <div class="form-group__item">
            <label for="docSeria">
              <span class="form-group__subtitle">Серия</span>
            </label>
            <input type="number" id="docSeria" v-model.trim="formReg.docSeria"
                   class="form-group__textfield">
          </div>

          <div class="form-group__item">
            <label for="docNumber">
              <span class="form-group__subtitle">Номер</span>
            </label>
            <input type="number" id="docNumber" v-model.trim="formReg.docNumber"
                   class="form-group__textfield">
          </div>

          <div class="form-group__item">
            <label for="whoGive">
              <span class="form-group__subtitle">Кто выдал</span>
            </label>
            <input type="text" id="whoGive" v-model.trim="formReg.whoGive"
                   class="form-group__textfield">
          </div>

          <div class="form-group__item">
            <label for="dateGive">
              <span class="form-group__subtitle form-group__subtitle_required">Дата выдачи</span>
            </label>
            <input type="date" id="dateGive" v-model.trim="formReg.dateGive"
                   class="form-group__textfield"
                   @blur="$v.formReg.dateGive.$touch()">
            <small v-if="$v.formReg.dateGive.$error">
              Введите дату выдачи Вашего документа
            </small>
          </div>

          <div class="form-group__buttons">
            <button type="button" @click="prevPart">Назад</button>
            <button type="submit">Завершить</button>
          </div>
        </div>
      </form>
      <div class="reg-complite" v-show="part===4">
        <h3>Регистрация завершена!</h3>
      </div>
    </div>
  </div>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators';

export default {
  data() {
    return {
      part: 1,

      formReg: {
        surName: '',
        name: '',
        thirdName: '',
        birthDay: '',
        phoneNumber: '',
        sex: '',
        clientGroup: [],
        doctor: '',
        mailing: '',
        mailIndex: '',
        country: '',
        region: '',
        city: '',
        street: '',
        houseNumber: '',
        docType: '',
        docSeria: '',
        docNumber: '',
        whoGive: '',
        dateGive: '',
      },
    };
  },
  methods: {
    nextPart() {
      // eslint-disable-next-line no-plusplus
      this.part++;
    },
    prevPart() {
      // eslint-disable-next-line no-plusplus
      this.part--;
    },
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        this.part = 1;
        return;
      }
      // eslint-disable-next-line no-plusplus
      this.part = 4;
    },
  },

  validations: {
    formReg: {
      surName: {
        required,
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      name: {
        required,
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      thirdName: {
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      birthDay: {
        required,
      },
      phoneNumber: {
        minLength: minLength(11),
        validData: (val) => /^7\d{10}$/.test(val),
      },
      mailIndex: {
        minLength: minLength(6),
        validData: (val) => /^\d{6}$/.test(val),
      },
      country: {
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      region: {
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      city: {
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      street: {
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      dateGive: {
        required,
      },
    },
  },
};
</script>

<style lang="sass">
body
  font-family: sans-serif
</style>

<style scoped lang="sass">

.container
  max-width: 300px
  width: 100%
  margin: 0 auto
.auth-form
  text-align: center

  .form-group
    display: flex
    flex-direction: column
    align-items: center

    &__item
      display: flex
      flex-direction: column
      align-items: center
      margin-bottom: 15px
      width: 80%
    &__subtitle
      &_required::after
        content: ' *'
        color: crimson

    &__textfield
      height: 30px
      width: 100%
      border: 1px solid #999
      border-radius: 3px
      font-size: 14px
      padding: 8px
      box-sizing: border-box
    &__sex-selection
      display: flex
      justify-content: space-around

    &__buttons
      width: 80%
      display: flex
      justify-content: space-around
  small
    color: crimson
    margin-top: 3px

  button
    border: none
    width: 45%
    padding: 10px
    box-sizing: border-box
    border-radius: 3px
    background-color: #0984e3
    color: #fff
    font-weight: bold
</style>
