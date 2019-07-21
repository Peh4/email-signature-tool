<template>
  <div class="formulaire">
    <div class="resultat">
      <table ref="copythis">
        <td class="logo">
          <img src="https://www.praxinova.fr/wp-content/uploads/2019/01/cropped-cabinet-de-qualité-de-vie-au-travail-90x62.png"/>
        </td>
        <td class="fl infos">
          <h1 :if="line1">{{line1}}</h1>
          <h2 :if="line2">{{line2}}</h2>
          <h2 :if="line3">{{line3}}</h2>
          <p class="mb">
            <a href="https://www.praxinova.fr" style="">https://www.praxinova.fr</a><br>
            <a :if="telephone1" :href="tel1">{{telephone1}}</a><br>
            <a :if="telephone2" :href="tel2">{{telephone2}}</a>
          </p>
          <h1>Praxinova</h1>
          <p>2 rue Marc Donadille<br>
          13013 Marseille</p>
        </td>
      </table>
    </div>
    <div class="champs">
      <p><button @click="selectText">Cliquez pour sélectionner la signature</button> puis -> copier coller pour configurer votre email</p>
      <p>
        <input class="line" type="text" v-model="line1" placeholder="Prénom Nom">
        <input class="line" type="text" v-model="line2" placeholder="titre 1">
        <input class="line" type="text" v-model="line3" placeholder="titre 2">
        <input class="line" type="text" v-model="telephone1" placeholder="téléphone 1">
        <input class="line" type="text" v-model="telephone2" placeholder="téléphone 2">
      </p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Formulaire',
  data () {
    return {
      line1: '',
      line2: '',
      line3: '',
      telephone1: '',
      telephone2: '',
      copythis: Object
    }
  },
  computed: {
    tel1: function () {
      return 'tel:' + this.telephone1.split(' ').join('')
    },
    tel2: function () {
      return 'tel:' + this.telephone2.split(' ').join('')
    },
    urlEncoded: function () {
      return encodeURI('line1=' + this.line1 + '&line2=' + this.line2 + '&line3=' + this.line3 + '&telephone1=' + this.telephone1 + '&telephone2=' + this.telephone2)
    }
  },
  mounted: function () {
    this.copythis = this.$refs.copythis
    this.line1 = this.$route.query.line1 ? this.$route.query.line1 : ''
    this.line2 = this.$route.query.line2 ? this.$route.query.line2 : ''
    this.line3 = this.$route.query.line3 ? this.$route.query.line3 : ''
    this.telephone1 = this.$route.query.telephone1 ? this.$route.query.telephone1 : ''
    this.telephone2 = this.$route.query.telephone2 ? this.$route.query.telephone2 : ''
  },
  watch: {
    urlEncoded: function () {
      this.$router.push({ query: { line1: this.line1, line2: this.line2, line3: this.line3, telephone1: this.telephone1, telephone2: this.telephone2 } })
    }
  },
  methods: {
    selectText: function () {
      if (document.selection) { // IE
        let range = document.body.createTextRange()
        range.moveToElementText(this.$refs.copythis)
        range.select()
      } else if (window.getSelection) {
        let range = document.createRange()
        range.selectNode(this.$refs.copythis)
        window.getSelection().removeAllRanges()
        window.getSelection().addRange(range)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.formulaire {
  font-size: 17px;
}
.mb {
  margin-bottom: 11px;
}
.champs {
  background: #f9be0b none;
  padding: 5%;
  margin-top: 10px;
  border-top: 2px solid #02a0a5;
  button {
    font-weight: 900;
  }
  p {
    color: #fff;
    font-weight: 900;
    padding-bottom: 20px;
  }
  input {
    display:block;
    width:90%;
    padding: 7px 9px;
  }
  .line {
    margin: 0 0 5px;
    font-size: 1.4rem;

  }
}
button {
  padding: 7px 9px;
  &:hover {
    cursor:pointer;
  }
}
.resultat {
  padding: 20px 20px 45px;
}

.fl {
  float: left;
}
.logo {
  vertical-align: top;
}
.infos {
  margin-top: 45px;
  padding-left: 11px;
  border-left: 2px solid #02a0a5;
}
h1, h2, h3, p, a {
  color: #02a0a5;
  text-decoration:none;
  padding:0;
  margin:0;
  font-family: helvetica, sans-serif;
  font-size: 1rem;
  line-height: 1.1rem;
}

h1, h2, h3 {
  font-weight: 900;
}

a:hover {
  color: #f9be0b;
}
</style>
