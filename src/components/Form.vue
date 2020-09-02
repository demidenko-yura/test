<template>
  <div>
    <form @submit.prevent='addClient'>
      <div class="block">
          <h1>Информация</h1>
          <span class="label">Фамилия<b>*</b></span>
          <input 
            name="surname" 
            placeholder="Введите вашу фамилию" 
            v-model.trim='formData.surname'
            :class="{errorClass: ($v.formData.surname.$dirty && !$v.formData.surname.required)}">

          <span class="label">Имя<b>*</b></span>
          <input 
            name="name" 
            placeholder="Введите ваше имя" 
            v-model.trim='formData.name'
            :class="{errorClass: ($v.formData.name.$dirty && !$v.formData.name.required)}">

          <span class="label">Отчество</span>
          <input name="middleName" placeholder="Введите ваше отчество" v-model='formData.middleName'>

          <span class="label">Дата рождения<b>*</b></span>
          <input 
            type="date" 
            name="dateOfBirthday" 
            v-model='formData.dateOfBirthday'
            :class="{errorClass: ($v.formData.dateOfBirthday.$dirty && !$v.formData.dateOfBirthday.required)}">

          <span class="label">Номер телефона<b>*</b></span>
          <input 
            name="phone"
            placeholder="Введите номер телефона" 
            v-model.number='formData.phone'
            :class="{errorClass: ($v.formData.phone.$dirty && !$v.formData.phone.required)}">

          <span class="label">Выберите пол<b></b></span>
          <span>
            <input id="female" type="radio" name="gender" value="Женский" v-model='formData.gender'>
            <label for="female">Женский</label>
            <input id="male" type="radio" name="gender" value="Мужской" v-model='formData.gender'>
            <label for="male">Мужской</label>   
          </span>

          <span class="label">Выберите группу клиентов<b>*</b></span>
          <select 
            multiple name="clientsGroup" 
            v-model='formData.clientsGroup'
            :class="{errorClass: ($v.formData.clientsGroup.$dirty && !$v.formData.clientsGroup.required)}">
            <option value='VIP'>VIP</option>
            <option value='Проблемные'>Проблемные</option>
            <option value='OMC'>OMC</option>
          </select>

          <span class="label">Выберите лечущего врача</span>
          <select name="DoctorName" v-model='formData.DoctorName'>
            <option value="Иванов">Иванов</option>
            <option value="Захаров">Захаров</option>
            <option value="Чернышева">Чернышева</option>
          </select> 

          <span>
            <input id="SMS" type="checkbox" name="SMS" v-model='formData.SMS'>
            <label for="SMS">Не отправлять СМС</label>
          </span>   
      </div>        

      <div class="block">
          <h1>Адрес</h1>

          <span class="label">Индекс</span>
          <input name="index" placeholder="Введите индекс" v-model.trim='formData.index'>

          <span class="label">Страна</span>
          <input name="country" placeholder="Введите страну" v-model.trim='formData.country'>

          <span class="label">Регион</span>
          <input name="region" placeholder="Введите регион" v-model.trim='formData.region'>

          <span class="label">Город<b>*</b></span>
          <input 
            name="town" 
            placeholder="Введите город" 
            v-model.trim='formData.town'
            :class="{errorClass: ($v.formData.town.$dirty && !$v.formData.town.required)}">

          <span class="label">Улица</span>
          <input name="street" placeholder="Введите название улицы" v-model='formData.street'>

          <span class="label">Дом</span>
          <input name="house" placeholder="Введите номер дома" v-model.trim='formData.house'>    
      </div>

      <div class="block">
          <h1>Паспорт</h1>

          <span class="label">Тип документа<b>*</b></span>
          <select 
            name="document" 
            v-model='formData.document' 
            :class="{errorClass: ($v.formData.document.$dirty && !$v.formData.document.required)}">
            <option value="Паспорт">Паспорт</option>
            <option value="Свидетельство о рождении">Свидетельство о рождении</option>
            <option value="Водительское удостоверение">Водительское удостоверение</option>
          </select>

          <span class="block_document" v-if=" formData.document === 'Паспорт' ">
            <span class="label">Серия</span>
            <input name="series" placeholder="Введите серию паспорта" v-model.trim='formData.series'>

            <span class="label">Номер</span>
            <input name="pasportNumber" placeholder="Введите номер паспорта" v-model.trim='formData.pasportNumber'>

            <span class="label">Кем выдан</span>
            <input name="issuedBy" placeholder="Введите кем выдан паспорт" v-model.trim='formData.issuedBy'>

            <span class="label">Дата выдачи</span>
            <input type="date"  name="dateOfIssue" placeholder="Введите дату выдачи паспорта" v-model.trim='formData.dateOfIssue'>             
          </span>

          <span class="block_document" v-if=" formData.document === 'Свидетельство о рождении' ">
            <span class="label">Свидетельство о рождении</span>
            <input name="birthCertificate" placeholder="Введите номер свидетельства" v-model.trim='formData.birthCertificate'>
          </span> 

          <span class="block_document" v-if=" formData.document === 'Водительское удостоверение' ">
            <span class="label">Номер водительского удостоверения</span>
            <input name="driveNumber" placeholder="Введите номер водительского" v-model.trim='formData.driveNumber'>
          </span>           
      </div>        

      <button type="submit">Создать</button>  
    </form>
    
    <div class="result">
      <ul v-for='(item, i) in clients'  v-bind:key="i">
        <h2>Информация</h2> 
        <li>
          Фамилия: {{item.surname}}
        </li>
        <li>
          Имя: {{item.name}}
        </li> 
        <li v-if="item.middleName">
          Отчество: {{item.middleName}}
        </li>      
        <li>
          Дата рождения: {{item.dateOfBirthday}}
        </li>  
        <li>
          Номер телефона: {{item.phone}}
        </li>   
        <li v-if="item.gender">
          Пол: {{item.gender}}
        </li> 
        <li>
          Группа клиентов: {{item.clientsGroup[0]}}
        </li>         
        <li v-if="item.DoctorName">
          Лечущий врач: {{item.DoctorName}}
        </li> 
        <li>
          Отправка СМС: {{item.SMS}}
        </li>

        <h4>Адрес</h4>  
        <li v-if="item.index">
          Индекс: {{item.index}}
        </li>
        <li v-if="item.country">
          Страна: {{item.country}}
        </li> 
        <li v-if="item.region">
          Регион: {{item.region}}
        </li>      
        <li>
          Город: {{item.town}}
        </li>  
        <li v-if="item.street">
          Улица: {{item.street}}
        </li>   
        <li v-if="item.house">
          Дом: {{item.house}}
        </li>   

        <h4>Данные</h4>  
        <li>
          Документ: {{item.document}}
        </li>

        <li v-if="item.series && item.document === 'Паспорт'">
          Серия: {{item.series}}
        </li> 
        <li v-if="item.pasportNumber && item.document === 'Паспорт'">
          Номер: {{item.pasportNumber}}
        </li>      
        <li v-if="item.issuedBy && item.document === 'Паспорт'">
          Кем выдан: {{item.issuedBy}}
        </li>  
        <li v-if="item.dateOfIssue && item.document === 'Паспорт'">
          Дата выдачи: {{item.dateOfIssue}}
        </li> 

        <li v-if="item.birthCertificate && item.document === 'Свидетельство о рождении'">
          Номер документа: {{item.birthCertificate}}
        </li>    
        
        <li v-if="item.driveNumber && item.document === 'Водительское удостоверение'">
          Номер документа: {{item.driveNumber}}
        </li>                                                    
      </ul>      
    </div>

  </div>
</template>

<script>
import {required} from 'vuelidate/lib/validators'


export default {
  data() {
    return {
      clients: [],
      formData: {
        surname: '',
        name: '',
        middleName: '',
        dateOfBirthday: '',
        phone: '',
        gender: '',
        clientsGroup: '',
        DoctorName: '',
        SMS: '',
        index: '',
        country: '',
        region: '',
        town: '',
        street: '',
        house: '',
        document: '',
        series: '',
        pasportNumber: '',
        issuedBy: '',
        dateOfIssue: '',

        birthCertificate: '',
        driveNumber: '',
      }
    }
  }, 


  validations: {
    formData: {
      surname: {required},
      name: {required},
      dateOfBirthday: {required},  
      phone: {required},
      clientsGroup: {required},
      town: {required},
      document: {required},          
    }
  },



  methods: {
    addClient() {
      console.log(this.$v)

      if (this.$v.formData.$invalid) {
        this.$v.$touch()
        alert('Заполните все необходимые поля')
        return
      }


      this.clients.push({
        surname: this.formData.surname,
        name: this.formData.name,
        middleName: this.formData.middleName,
        dateOfBirthday: this.formData.dateOfBirthday,
        phone: this.formData.phone,
        gender: this.formData.gender,
        clientsGroup: this.formData.clientsGroup != 'Выберите группу клиентов' ? this.formData.clientsGroup : null,
        DoctorName: this.formData.DoctorName != 'Выберите врача' ? this.formData.DoctorName : null,
        SMS: this.formData.SMS === true ? 'Не Согласен' : 'Согласен',
        index: this.formData.index,
        country: this.formData.country,
        region: this.formData.region,
        town: this.formData.town,
        street: this.formData.street,
        house: this.formData.house,
        document: this.formData.document,
        
        series: this.formData.series,
        pasportNumber: this.formData.pasportNumber,
        issuedBy: this.formData.issuedBy,
        dateOfIssue: this.formData.dateOfIssue,

        birthCertificate: this.formData.birthCertificate,
        driveNumber: this.formData.driveNumber,
      })

      console.log(this.clients)
      alert('Клиент успешно создан!')


      for(let key in this.formData) {
        this.formData[key] = null
      }
      this.$v.$reset()
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
